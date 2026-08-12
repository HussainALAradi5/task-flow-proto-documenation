# API Reference

## Base URL

```
http://localhost:5000/api
```

## Authentication

All protected endpoints require a JWT token in the `Authorization` header:

```
Authorization: Bearer <token>
```

## Response Format

### Success

```json
{
  "status": "success",
  "data": {}
}
```

### Success with Token

```json
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "data": {}
}
```

### Error

```json
{
  "status": "error",
  "message": "Error description"
}
```

### Validation Error

```json
{
  "status": "error",
  "message": "Validation failed",
  "errors": [
    {
      "field": "body.email",
      "message": "Invalid email"
    }
  ]
}
```

---

## User Endpoints

### Signup

```
POST /api/users
```

**Public:** Yes

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| userName | string | Yes | Unique username |
| email | string | Yes | Unique email |
| password | string | Yes | Plain text (hashed before storage) |
| mobileNumber | string | No | Phone number |

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "_id": "64f1a2b3c4d5e6f7a8b9c0d1",
    "userName": "john_doe",
    "email": "john@example.com",
    "role": "Member",
    "isActive": true,
    "createdAt": "2026-08-12T10:00:00.000Z"
  }
}
```

### Login

```
POST /api/users/login
```

**Public:** Yes

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| email | string | Yes | Registered email |
| password | string | Yes | Plain text password |

**Response (200):**
```json
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "data": {
    "_id": "64f1a2b3c4d5e6f7a8b9c0d1",
    "userName": "john_doe",
    "email": "john@example.com",
    "role": "Member"
  }
}
```

### Get All Users

```
GET /api/users
```

**Public:** No (requires auth)

**Notes:** Admin sees all users, others see only their created records.

**Response (200):**
```json
{
  "status": "success",
  "data": [
    {
      "_id": "...",
      "userName": "john_doe",
      "email": "john@example.com",
      "role": "Member",
      "teamId": null,
      "isActive": true
    }
  ]
}
```

### Get User by ID

```
GET /api/users/:id
```

**Public:** No

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

### Update User

```
PATCH /api/users/:id
```

**Public:** No

**Request Body:** Partial user fields

**Response (200):**
```json
{
  "status": "success",
  "data": { "..." : "updated user" }
}
```

### Update User Role

```
PATCH /api/users/:id/role
```

**Public:** No

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| role | string | Yes | `Admin`, `Leader`, or `Member` |

**Response (200):**
```json
{
  "status": "success",
  "data": {
    "_id": "...",
    "userName": "john_doe",
    "role": "Leader"
  }
}
```

### Delete User

```
DELETE /api/users/:id
```

**Public:** No

**Notes:** Soft delete (sets `isActive: false`)

**Response (200):**
```json
{
  "status": "success",
  "message": "Resource deactivated successfully"
}
```

---

## Team Endpoints

### Create Team

```
POST /api/teams
```

**Auth:** Required

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| name | string | Yes | Team name |
| description | string | No | Team description |

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "_id": "...",
    "name": "Frontend Team",
    "description": "UI/UX development",
    "isActive": true,
    "createdBy": "user_id"
  }
}
```

### Get My Teams

```
GET /api/teams
```

**Auth:** Required

**Notes:** Admin sees all teams, others see only teams they created.

**Response (200):**
```json
{
  "status": "success",
  "data": [
    {
      "_id": "...",
      "name": "Frontend Team",
      "description": "UI/UX development",
      "isActive": true
    }
  ]
}
```

### Get Team by ID

```
GET /api/teams/:id
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "data": { "..." : "team" }
}
```

### Update Team

```
PATCH /api/teams/:id
```

**Auth:** Required

**Request Body:** Partial team fields

**Response (200):**
```json
{
  "status": "success",
  "data": { "..." : "updated team" }
}
```

### Delete Team

```
DELETE /api/teams/:id
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "message": "Resource deactivated successfully"
}
```

---

## Project Endpoints

### Create Project

```
POST /api/projects
```

**Auth:** Required

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| title | string | Yes | Project title |
| description | string | No | Project description |
| teamId | ObjectId | No | Associated team |

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "_id": "...",
    "title": "TaskFlow Frontend",
    "description": "Angular client app",
    "teamId": "team_id",
    "createdBy": "user_id",
    "createdAt": "2026-08-12T10:00:00.000Z"
  }
}
```

**Notes:** Creating a project auto-promotes the creator from `Member` to `Leader`.

### Get My Projects

```
GET /api/projects
```

**Auth:** Required

**Notes:** Admin sees all projects, others see only their created projects.

**Response (200):**
```json
{
  "status": "success",
  "data": [
    {
      "_id": "...",
      "title": "TaskFlow Frontend",
      "description": "Angular client app",
      "teamId": "team_id"
    }
  ]
}
```

### Get Project by ID

```
GET /api/projects/:id
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "data": { "..." : "project" }
}
```

### Update Project

```
PATCH /api/projects/:id
```

**Auth:** Required

**Request Body:** Partial project fields

**Response (200):**
```json
{
  "status": "success",
  "data": { "..." : "updated project" }
}
```

### Delete Project

```
DELETE /api/projects/:id
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "message": "Resource deactivated successfully"
}
```

---

## Task Endpoints

### Create Task

```
POST /api/tasks
```

**Auth:** Required

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| title | string | Yes | Task title |
| description | string | No | Task description |
| status | string | No | `To Do`, `In Progress`, `In Review`, `Done` |
| priority | string | No | `Low`, `Medium`, `High`, `Critical` |
| projectId | ObjectId | Yes | Parent project |
| milestoneId | ObjectId | No | Parent milestone |
| assignTo | ObjectId | No | Assigned user |

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "_id": "...",
    "title": "Implement login page",
    "description": "Create Angular login component",
    "status": "To Do",
    "priority": "Medium",
    "projectId": "project_id",
    "milestoneId": null,
    "assignTo": "user_id",
    "createdBy": "user_id"
  }
}
```

### Get My Tasks

```
GET /api/tasks
```

**Auth:** Required

**Notes:** Admin sees all tasks, others see only their created tasks.

### Get Tasks by Project

```
GET /api/tasks/project/:projectId
```

**Auth:** Required

**Notes:** Admin sees all project tasks, others see only their tasks within the project.

**Response (200):**
```json
{
  "status": "success",
  "data": [
    {
      "_id": "...",
      "title": "Implement login page",
      "status": "In Progress",
      "priority": "High",
      "assignTo": { "_id": "...", "userName": "john_doe" }
    }
  ]
}
```

### Get Tasks by Milestone

```
GET /api/tasks/milestone/:milestoneId
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "data": [ "..." ]
}
```

### Get Task by ID

```
GET /api/tasks/:id
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "data": { "..." : "task" }
}
```

### Update Task

```
PATCH /api/tasks/:id
```

**Auth:** Required

**Request Body:** Partial task fields (status, priority, assignTo, etc.)

**Response (200):**
```json
{
  "status": "success",
  "data": { "..." : "updated task" }
}
```

### Delete Task

```
DELETE /api/tasks/:id
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "message": "Resource deactivated successfully"
}
```

---

## Milestone Endpoints

### Create Milestone

```
POST /api/milestones
```

**Auth:** Required

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| name | string | Yes | Milestone name |
| projectId | ObjectId | Yes | Parent project |

**Response (201):**
```json
{
  "status": "success",
  "data": {
    "_id": "...",
    "name": "Sprint 1",
    "projectId": "project_id",
    "createdBy": "user_id"
  }
}
```

### Get My Milestones

```
GET /api/milestones
```

**Auth:** Required

### Get Milestones by Project

```
GET /api/milestones/project/:projectId
```

**Auth:** Required

**Response (200):**
```json
{
  "status": "success",
  "data": [
    {
      "_id": "...",
      "name": "Sprint 1",
      "projectId": "project_id"
    }
  ]
}
```

### Get Milestone by ID

```
GET /api/milestones/:id
```

**Auth:** Required

### Update Milestone

```
PATCH /api/milestones/:id
```

**Auth:** Required

### Delete Milestone

```
DELETE /api/milestones/:id
```

**Auth:** Required

---

## Event Endpoints

### Create Event

```
POST /api/events
```

**Auth:** Required

**Request Body:**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| title | string | Yes | Event title |
| description | string | No | Event description |
| entityType | string | Yes | `User`, `Team`, `Task`, `Project`, `Milestone` |
| entityId | ObjectId | Yes | ID of the related entity |

### Get All Events

```
GET /api/events
```

**Auth:** Required

### Get Event by ID

```
GET /api/events/:id
```

**Auth:** Required

### Update Event

```
PATCH /api/events/:id
```

**Auth:** Required

### Delete Event

```
DELETE /api/events/:id
```

**Auth:** Required

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Bad request / Validation error |
| 401 | Unauthorized (no token, invalid token, expired token) |
| 403 | Forbidden (insufficient permissions) |
| 404 | Resource not found |
| 500 | Internal server error |

## Health Check

```
GET /
```

**Response:**
```json
{
  "message": "TaskFlowProto TypeScript API is running..."
}
```
