# Server-Side Models

## Overview

MongoDB schemas with Mongoose ODM. All models extend `IBaseEntity` with common fields.

## Base Entity

Every model includes:

```typescript
interface IBaseEntity {
  id: string;
  code: string;           // Unique identifier
  createdBy?: ObjectId;   // Ref → User
  updatedBy?: ObjectId;   // Ref → User
  createdAt: Date;
  updatedAt: Date;
}
```

---

## User

**Collection:** `users`

| Field | Type | Required | Unique | Default | Ref |
|-------|------|----------|--------|---------|-----|
| userName | String | Yes | Yes | - | - |
| password | String | Yes | No | - | - |
| email | String | Yes | Yes | - | - |
| mobileNumber | String | No | No | `""` | - |
| teamId | ObjectId | No | No | `null` | Team |
| role | String | No | No | `Member` | - |
| isActive | Boolean | No | No | `true` | - |

**Enum:** `UserRole` = `Admin`, `Leader`, `Member`

---

## Team

**Collection:** `teams`

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| name | String | Yes | - | Team name |
| description | String | No | `""` | Description |
| isActive | Boolean | No | `true` | Soft delete |

---

## Project

**Collection:** `projects`

| Field | Type | Required | Default | Ref |
|-------|------|----------|---------|-----|
| title | String | Yes | - | - |
| description | String | No | `""` | - |
| teamId | ObjectId | No | `null` | Team |

---

## Task

**Collection:** `tasks`

| Field | Type | Required | Default | Ref |
|-------|------|----------|---------|-----|
| title | String | Yes | - | - |
| description | String | No | `""` | - |
| status | String | No | `To Do` | - |
| priority | String | No | `Medium` | - |
| projectId | ObjectId | Yes | - | Project |
| milestoneId | ObjectId | No | `null` | Milestone |
| assignTo | ObjectId | No | `null` | User |
| lastAssignTo | ObjectId | No | `null` | User |

**Enums:**
- `GenericStatus`: `To Do`, `In Progress`, `In Review`, `Done`
- `TaskPriority`: `Low`, `Medium`, `High`, `Critical`

---

## Milestone

**Collection:** `milestones`

| Field | Type | Required | Ref |
|-------|------|----------|-----|
| name | String | Yes | - |
| projectId | ObjectId | Yes | Project |

---

## Event

**Collection:** `events`

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| title | String | Yes | Event title |
| description | String | No | Details |
| entityType | String | Yes | Entity type |
| entityId | ObjectId | Yes | Polymorphic ref |

**Enum:** `EntityType` = `User`, `Team`, `Task`, `Project`, `Milestone`

---

## Enums

### UserRole
```typescript
enum UserRole {
  ADMIN = 'Admin',
  LEADER = 'Leader',
  MEMBER = 'Member'
}
```

### GenericStatus
```typescript
enum GenericStatus {
  TODO = 'To Do',
  IN_PROGRESS = 'In Progress',
  IN_REVIEW = 'In Review',
  DONE = 'Done'
}
```

### TaskPriority
```typescript
enum TaskPriority {
  LOW = 'Low',
  MEDIUM = 'Medium',
  HIGH = 'High',
  CRITICAL = 'Critical'
}
```

### EntityType
```typescript
enum EntityType {
  USER = 'User',
  TEAM = 'Team',
  TASK = 'Task',
  PROJECT = 'Project',
  MILESTONE = 'Milestone'
}
```

---

## Relationships

```
User 1:N Team (teamId)
Team 1:N Project (teamId)
Project 1:N Task (projectId)
Project 1:N Milestone (projectId)
Milestone 1:N Task (milestoneId)
User 1:N Task (assignTo, createdBy)
Any 1:N Event (entityType + entityId)
```
