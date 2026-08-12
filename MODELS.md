# Data Models

## Overview

TaskFlow Proto uses **MongoDB** with **Mongoose** ODM. All models share a common base schema and follow consistent patterns.

## Base Entity

Every model extends `IBaseEntity` and includes these fields:

```typescript
interface IBaseEntity extends mongoose.Document {
  id: string;
  __v: number;
  code: string;           // Unique identifier string
  createdBy?: Types.ObjectId;  // Reference to User
  updatedBy?: Types.ObjectId;  // Reference to User
  createdAt: Date;
  updatedAt: Date;
}
```

**Base Schema Fields:**
```typescript
const baseSchemaFields = {
  code: { type: String, required: true, unique: true },
  createdBy: { type: Schema.Types.ObjectId, ref: 'User', default: null },
  updatedBy: { type: Schema.Types.ObjectId, ref: 'User', default: null },
};
```

---

## User

**Collection:** `users`

```typescript
interface IUser extends IBaseEntity {
  userName: string;
  password?: string;
  email: string;
  mobileNumber?: string;
  teamId?: Schema.Types.ObjectId;
  role: UserRole;
  isActive: boolean;
}
```

| Field | Type | Required | Unique | Default | Description |
|-------|------|----------|--------|---------|-------------|
| userName | String | Yes | Yes | - | Display name |
| password | String | Yes | No | - | Bcrypt hashed |
| email | String | Yes | Yes | - | Login identifier |
| mobileNumber | String | No | No | `""` | Contact number |
| teamId | ObjectId | No | No | `null` | Ref → Team |
| role | String | No | No | `Member` | `Admin`, `Leader`, `Member` |
| isActive | Boolean | No | No | `true` | Soft delete flag |

**Indexes:** `userName` (unique), `email` (unique)

---

## Team

**Collection:** `teams`

```typescript
interface ITeam extends IBaseEntity {
  name: string;
  description?: string;
  isActive: boolean;
}
```

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| name | String | Yes | - | Team name |
| description | String | No | `""` | Team description |
| isActive | Boolean | No | `true` | Soft delete flag |

---

## Project

**Collection:** `projects`

```typescript
interface IProject extends IBaseEntity {
  title: string;
  description?: string;
  teamId?: Schema.Types.ObjectId;
}
```

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| title | String | Yes | - | Project name |
| description | String | No | `""` | Project description |
| teamId | ObjectId | No | `null` | Ref → Team |

**Relationships:**
- `teamId` → Team (optional)
- `createdBy` → User (creator/leader)

---

## Task

**Collection:** `tasks`

```typescript
interface ITask extends IBaseEntity {
  title: string;
  description?: string;
  status: GenericStatus;
  priority: TaskPriority;
  projectId: Schema.Types.ObjectId;
  milestoneId?: Schema.Types.ObjectId;
  assignTo?: Schema.Types.ObjectId;
  lastAssignTo?: Schema.Types.ObjectId;
}
```

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| title | String | Yes | - | Task title |
| description | String | No | `""` | Task description |
| status | String | No | `To Do` | Task status |
| priority | String | No | `Medium` | Task priority |
| projectId | ObjectId | Yes | - | Ref → Project |
| milestoneId | ObjectId | No | `null` | Ref → Milestone |
| assignTo | ObjectId | No | `null` | Ref → User (assigned) |
| lastAssignTo | ObjectId | No | `null` | Ref → User (previous) |

**Relationships:**
- `projectId` → Project (required)
- `milestoneId` → Milestone (optional)
- `assignTo` → User (optional)
- `lastAssignTo` → User (optional)
- `createdBy` → User (creator)

---

## Milestone

**Collection:** `milestones`

```typescript
interface IMilestone extends IBaseEntity {
  name: string;
  projectId: Schema.Types.ObjectId;
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| name | String | Yes | Milestone name |
| projectId | ObjectId | Yes | Ref → Project |

**Relationships:**
- `projectId` → Project (required)
- `createdBy` → User (creator)

---

## Event

**Collection:** `events`

```typescript
interface IEvent extends IBaseEntity {
  title: string;
  description?: string;
  entityType: EntityType;
  entityId: Schema.Types.ObjectId;
}
```

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| title | String | Yes | - | Event title |
| description | String | No | `""` | Event details |
| entityType | String | Yes | - | Entity type |
| entityId | ObjectId | Yes | - | Polymorphic reference |

**Entity Types:** `User`, `Team`, `Task`, `Project`, `Milestone`

**Usage:** Generic audit log that can reference any entity type via `entityType` + `entityId`.

---

## Enums

### UserRole

```typescript
enum UserRole {
  ADMIN = 'Admin',
  LEADER = 'Leader',
  MEMBER = 'Member',
}
```

### GenericStatus (Task Status)

```typescript
enum GenericStatus {
  TODO = 'To Do',
  IN_PROGRESS = 'In Progress',
  IN_REVIEW = 'In Review',
  DONE = 'Done',
}
```

### TaskPriority

```typescript
enum TaskPriority {
  LOW = 'Low',
  MEDIUM = 'Medium',
  HIGH = 'High',
  CRITICAL = 'Critical',
}
```

### EntityType

```typescript
enum EntityType {
  USER = 'User',
  TEAM = 'Team',
  TASK = 'Task',
  PROJECT = 'Project',
  MILESTONE = 'Milestone',
}
```

---

## Entity Relationship Diagram

```
┌──────────┐       ┌──────────┐       ┌──────────┐
│   User   │◄──────│   Team   │◄──────│  Project │
└──────────┘       └──────────┘       └──────────┘
     │                                      │
     │ createdBy                            │ projectId
     │ assignTo                             │
     ▼                                      ▼
┌──────────┐       ┌──────────┐       ┌──────────┐
│   Task   │──────►│Milestone │──────►│  Event   │
└──────────┘       └──────────┘       └──────────┘
     │
     │ milestoneId
     ▼
┌──────────┐
│ Milestone │
└──────────┘
```

**Key Relationships:**
- User `1:N` Team (via `teamId`)
- Team `1:N` Project (via `teamId`)
- Project `1:N` Task (via `projectId`)
- Project `1:N` Milestone (via `projectId`)
- Milestone `1:N` Task (via `milestoneId`)
- User `1:N` Task (via `assignTo`, `createdBy`)
- Any Entity `1:N` Event (via `entityType` + `entityId`)

---

## Soft Delete Pattern

All models use `isActive: false` instead of actual document deletion:

```typescript
// BaseService.softDelete
async softDelete(id: string): Promise<T | null> {
  return await this.model
    .findByIdAndUpdate(id, { isActive: false }, { new: true })
    .exec();
}
```

**Querying active records:**
```typescript
// Only return active records
const activeItems = await Model.find({ isActive: true });
```
