# Server-Side Endpoints

## Overview

REST API endpoints with role-based access control and Zod validation.

## Base URL

```
http://localhost:5000/api
```

## Response Format

```json
{
  "status": "success | error",
  "data": {},
  "pagination": { "page": 1, "limit": 10, "total": 42, "totalPages": 5 }
}
```

---

## Auth Endpoints

| Method | Endpoint | Auth | Roles | Validation |
|--------|----------|------|-------|------------|
| `POST` | `/users/signup` | No | Public | `signupSchema` |
| `POST` | `/users/login` | No | Public | `loginSchema` |

---

## User Endpoints

| Method | Endpoint | Auth | Roles | Validation |
|--------|----------|------|-------|------------|
| `GET` | `/users` | Yes | Admin | - |
| `GET` | `/users/profile` | Yes | All | - |
| `GET` | `/users/:id` | Yes | Admin | - |
| `PATCH` | `/users/:id` | Yes | Admin | `updateUserSchema` |
| `PATCH` | `/users/:id/role` | Yes | Admin | `updateRoleSchema` |
| `DELETE` | `/users/:id` | Yes | Admin | - |

---

## Team Endpoints

| Method | Endpoint | Auth | Roles | Validation |
|--------|----------|------|-------|------------|
| `POST` | `/teams` | Yes | Admin, Leader | `createTeamSchema` |
| `GET` | `/teams` | Yes | All | - |
| `GET` | `/teams/:id` | Yes | All | - |
| `PATCH` | `/teams/:id` | Yes | Admin, Leader | `updateTeamSchema` |
| `DELETE` | `/teams/:id` | Yes | Admin | - |

---

## Project Endpoints

| Method | Endpoint | Auth | Roles | Validation |
|--------|----------|------|-------|------------|
| `POST` | `/projects` | Yes | Admin, Leader | `createProjectSchema` |
| `GET` | `/projects` | Yes | All | - |
| `GET` | `/projects/:id` | Yes | All | - |
| `PATCH` | `/projects/:id` | Yes | Admin, Leader | `updateProjectSchema` |
| `DELETE` | `/projects/:id` | Yes | Admin | - |

---

## Milestone Endpoints

| Method | Endpoint | Auth | Roles | Validation |
|--------|----------|------|-------|------------|
| `POST` | `/milestones` | Yes | Admin, Leader | `createMilestoneSchema` |
| `GET` | `/milestones` | Yes | All | - |
| `GET` | `/milestones/project/:projectId` | Yes | All | - |
| `GET` | `/milestones/:id` | Yes | All | - |
| `PATCH` | `/milestones/:id` | Yes | Admin, Leader | `updateMilestoneSchema` |
| `DELETE` | `/milestones/:id` | Yes | Admin, Leader | - |

---

## Task Endpoints

| Method | Endpoint | Auth | Roles | Validation |
|--------|----------|------|-------|------------|
| `POST` | `/tasks` | Yes | Admin, Leader | `createTaskSchema` |
| `GET` | `/tasks` | Yes | All | - |
| `GET` | `/tasks/project/:projectId` | Yes | All | - |
| `GET` | `/tasks/milestone/:milestoneId` | Yes | All | - |
| `GET` | `/tasks/:id` | Yes | All | - |
| `PATCH` | `/tasks/:id` | Yes | Admin, Leader | `updateTaskSchema` |
| `DELETE` | `/tasks/:id` | Yes | Admin, Leader | - |

---

## Event Endpoints

| Method | Endpoint | Auth | Roles | Validation |
|--------|----------|------|-------|------------|
| `POST` | `/events` | Yes | Admin, Leader | `createEventSchema` |
| `GET` | `/events` | Yes | All | - |
| `GET` | `/events/:id` | Yes | All | - |
| `PATCH` | `/events/:id` | Yes | Admin | `updateEventSchema` |
| `DELETE` | `/events/:id` | Yes | Admin | - |

---

## Pagination

All list endpoints support pagination via query params:

```
GET /api/tasks?page=1&limit=10
```

| Param | Default | Min | Max | Description |
|-------|---------|-----|-----|-------------|
| `page` | 1 | 1 | - | Page number |
| `limit` | 10 | 1 | 100 | Items per page |

**Response:**
```json
{
  "status": "success",
  "data": [...],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 42,
    "totalPages": 5
  }
}
```

---

## Validation Schemas

### User

```typescript
signupSchema: { userName, email, password, mobileNumber? }
loginSchema: { email, password }
updateUserSchema: { userName?, email?, mobileNumber?, teamId? }
updateRoleSchema: { role: 'Admin' | 'Leader' | 'Member' }
```

### Team

```typescript
createTeamSchema: { name, description? }
updateTeamSchema: { name?, description? }
```

### Project

```typescript
createProjectSchema: { title, description?, teamId? }
updateProjectSchema: { title?, description?, teamId? }
```

### Task

```typescript
createTaskSchema: { title, description?, status?, priority?, projectId, milestoneId?, assignTo? }
updateTaskSchema: { title?, description?, status?, priority?, milestoneId?, assignTo? }
```

### Milestone

```typescript
createMilestoneSchema: { name, projectId }
updateMilestoneSchema: { name? }
```

### Event

```typescript
createEventSchema: { title, description?, entityType, entityId }
updateEventSchema: { title?, description? }
```
