# Authentication

## Overview

TaskFlow Proto uses **JWT (JSON Web Token)** for stateless authentication. Passwords are hashed with **bcrypt** before storage.

## Auth Flow

```
┌─────────┐     POST /api/users      ┌─────────┐
│  Client  │ ──────────────────────→  │  Server  │
│          │    { email, password }    │          │
│          │ ←──────────────────────  │          │
│          │    { token, user }       │          │
└─────────┘                          └─────────┘
     │
     │  GET /api/projects
     │  Authorization: Bearer <token>
     │
     ▼
┌─────────┐     JWT Verify           ┌─────────┐
│  Server  │ ──────────────────────→  │  JWT lib │
│          │ ←──────────────────────  │          │
│          │    decoded { id }        │          │
└─────────┘                          └─────────┘
     │
     ▼
┌─────────┐     Find User by ID      ┌─────────┐
│  Server  │ ──────────────────────→  │  MongoDB │
│          │ ←──────────────────────  │          │
│          │    user document         │          │
└─────────┘                          └─────────┘
     │
     ▼
  req.user = currentUser
  next()
```

## Endpoints

### Signup

```
POST /api/users
```

**Request Body:**
```json
{
  "userName": "john_doe",
  "email": "john@example.com",
  "password": "secret123",
  "mobileNumber": "+1234567890"
}
```

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "_id": "...",
    "userName": "john_doe",
    "email": "john@example.com",
    "role": "Member",
    "isActive": true
  }
}
```

**Notes:**
- Password is automatically hashed (bcrypt, salt rounds: 10)
- Default role is `Member`
- `code` field is auto-generated

### Login

```
POST /api/users/login
```

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "secret123"
}
```

**Response (200):**
```json
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "data": {
    "_id": "...",
    "userName": "john_doe",
    "email": "john@example.com",
    "role": "Member"
  }
}
```

**Error (401):**
```json
{
  "status": "error",
  "message": "Invalid email or password"
}
```

### Get Profile

```
GET /api/users/profile
```

**Headers:**
```
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "_id": "...",
    "userName": "john_doe",
    "email": "john@example.com",
    "role": "Member",
    "teamId": null,
    "isActive": true
  }
}
```

## JWT Structure

### Token Payload

```json
{
  "id": "user_id",
  "iat": 1691234567,
  "exp": 1693826567
}
```

### Configuration

| Setting | Default | Environment Variable |
|---------|---------|---------------------|
| Secret | `super-secret-trello-clone-key` | `JWT_SECRET` |
| Expiry | `30d` | `JWT_EXPIRES_IN` |

## Middleware

### protect

Extracts and verifies JWT from `Authorization: Bearer <token>` header.

```typescript
// Applied globally to protected routes
router.use(protect);
```

**Flow:**
1. Extract token from `Authorization` header
2. Verify token with `jwt.verify()`
3. Find user by decoded `id`
4. Attach user to `req.user`
5. Call `next()`

**Errors:**
- `401` - No token provided
- `401` - User no longer exists
- `401` - Invalid/expired token

### restrictTo

Role-based authorization middleware.

```typescript
// Usage example
router.post('/', protect, restrictTo('Admin', 'Leader'), controller.create);
```

**Errors:**
- `403` - User role not in allowed roles

## Password Security

- **Hashing:** bcrypt with 10 salt rounds
- **Storage:** Only hashed password stored in MongoDB
- **Comparison:** `bcrypt.compare()` during login
- **Selection:** Password field excluded by default, explicitly selected with `.select('+password')` during auth

## Token Lifecycle

```
Signup → Password hashed → User created
    ↓
Login → Credentials verified → JWT signed (30d expiry) → Token returned
    ↓
Request → Token in header → JWT verified → User loaded → req.user set
    ↓
Protected Route → check req.user exists → proceed
    ↓
Role Check → restrictTo middleware → verify role → proceed or 403
```
