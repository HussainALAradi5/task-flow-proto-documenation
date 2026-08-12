# Server-Side Services

## Overview

Services contain business logic and data access. All services extend `BaseService<T>` which provides generic CRUD operations with event logging.

## Service Architecture

```
BaseService<T>
├── UserService      - User auth, roles, password hashing
├── TeamService      - Team CRUD with event logging
├── ProjectService   - Project CRUD + auto role promotion
├── TaskService      - Task CRUD + filter builders
├── MilestoneService - Milestone CRUD + filter builders
└── EventService     - Audit log with logEvent helper
```

---

## BaseService\<T\>

**Location:** `src/services/BaseService.ts`

Generic service providing CRUD operations for any Mongoose model.

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<T>): Promise<T>` | Create new document |
| `getById` | `(id: string): Promise<T \| null>` | Find by ID |
| `getAll` | `(filter?): Promise<T[]>` | Find all with filter |
| `getAllPaginated` | `(filter, params): Promise<PaginatedResult<T>>` | Paginated find |
| `update` | `(id, data): Promise<T \| null>` | Update document |
| `softDelete` | `(id): Promise<T \| null>` | Set `isActive: false` |

---

## UserService

**Location:** `src/services/user/UserService.ts`
**Model:** User
**Extends:** `BaseService<IUser>`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<IUser>): Promise<IUser>` | Hash password, assign default role, log event |
| `update` | `(id, data): Promise<IUser \| null>` | Update user, log event |
| `authenticate` | `(email, password): Promise<IUser \| null>` | Verify credentials with bcrypt |
| `findByEmailOrUsername` | `(email, userName): Promise<IUser \| null>` | Check uniqueness |
| `assignRole` | `(userId, role): Promise<IUser \| null>` | Change role, log event |
| `promoteToLeaderForNewProject` | `(userId): Promise<IUser \| null>` | Auto-promote Member to Leader |

### Business Logic

- **Password Hashing:** bcrypt with 10 salt rounds
- **Default Role:** `Member` on signup
- **Auto-Promotion:** Creating a project promotes `Member` → `Leader`
- **Event Logging:** Create, update, role changes

---

## TeamService

**Location:** `src/services/team/TeamService.ts`
**Model:** Team
**Extends:** `BaseService<ITeam>`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<ITeam>): Promise<ITeam>` | Create team, log event |
| `update` | `(id, data): Promise<ITeam \| null>` | Update team, log event |
| `softDelete` | `(id): Promise<ITeam \| null>` | Deactivate team, log event |

### Business Logic

- **Event Logging:** Create, update, deactivate
- **Inherited CRUD:** getAll, getById from BaseService

---

## ProjectService

**Location:** `src/services/project/ProjectService.ts`
**Model:** Project
**Extends:** `BaseService<IProject>`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `createProject` | `(data: Partial<IProject>): Promise<IProject>` | Create project + auto-promote creator |
| `update` | `(id, data): Promise<IProject \| null>` | Update project, log event |
| `softDelete` | `(id): Promise<IProject \| null>` | Deactivate project, log event |

### Business Logic

- **Auto-Promotion:** Creator becomes `Leader` if currently `Member`
- **Event Logging:** Create, update, deactivate

---

## TaskService

**Location:** `src/services/project/TaskService.ts`
**Model:** Task
**Extends:** `BaseService<ITask>`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<ITask>): Promise<ITask>` | Create task, log event |
| `update` | `(id, data): Promise<ITask \| null>` | Update task, log event |
| `softDelete` | `(id): Promise<ITask \| null>` | Deactivate task, log event |
| `buildProjectFilter` | `(projectId): QueryFilter<ITask>` | Filter tasks by project |
| `buildProjectUserFilter` | `(projectId, userId): QueryFilter<ITask>` | Filter by project + creator |
| `buildMilestoneFilter` | `(milestoneId): QueryFilter<ITask>` | Filter tasks by milestone |
| `buildMilestoneUserFilter` | `(milestoneId, userId): QueryFilter<ITask>` | Filter by milestone + creator |

### Business Logic

- **Filter Builders:** Type-safe query construction
- **Event Logging:** Create, update, deactivate

---

## MilestoneService

**Location:** `src/services/project/MilestoneService.ts`
**Model:** Milestone
**Extends:** `BaseService<IMilestone>`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<IMilestone>): Promise<IMilestone>` | Create milestone, log event |
| `update` | `(id, data): Promise<IMilestone \| null>` | Update milestone, log event |
| `softDelete` | `(id): Promise<IMilestone \| null>` | Deactivate milestone, log event |
| `buildProjectFilter` | `(projectId): QueryFilter<IMilestone>` | Filter by project |
| `buildProjectUserFilter` | `(projectId, userId): QueryFilter<IMilestone>` | Filter by project + creator |

---

## EventService

**Location:** `src/services/EventService.ts`
**Model:** Event
**Extends:** `BaseService<IEvent>`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `logEvent` | `(title, entityType, entityId, description?, userId?): Promise<IEvent>` | Create audit log entry |

### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `title` | `string` | Event title (e.g., "Task created") |
| `entityType` | `EntityType` | `User`, `Team`, `Task`, `Project`, `Milestone` |
| `entityId` | `string` | ID of the related entity |
| `description` | `string` | Optional details |
| `userId` | `string` | Optional user who triggered the event |

### Auto-Logged Events

Every service logs events automatically on:
- **Create:** `{Entity} created`
- **Update:** `{Entity} updated`
- **Delete (soft):** `{Entity} deactivated`
- **Role change:** `User role updated`
