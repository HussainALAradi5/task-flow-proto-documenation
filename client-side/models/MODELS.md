# Client-Side Models

## Overview

TypeScript interfaces for Angular services and components.

## Location

```
src/app/core/models/
├── user.model.ts
├── team.model.ts
├── project.model.ts
├── task.model.ts
├── milestone.model.ts
├── event.model.ts
└── pagination.model.ts
```

---

## User Model

```typescript
// src/app/core/models/user.model.ts

export interface User {
  _id: string;
  userName: string;
  email: string;
  mobileNumber?: string;
  teamId?: string;
  role: UserRole;
  isActive: boolean;
  createdAt: string;
  updatedAt: string;
}

export enum UserRole {
  ADMIN = 'Admin',
  LEADER = 'Leader',
  MEMBER = 'Member'
}

export interface SignupRequest {
  userName: string;
  email: string;
  password: string;
  mobileNumber?: string;
}

export interface LoginRequest {
  email: string;
  password: string;
}

export interface AuthResponse {
  status: string;
  token: string;
  data: User;
}
```

---

## Team Model

```typescript
// src/app/core/models/team.model.ts

export interface Team {
  _id: string;
  name: string;
  description?: string;
  isActive: boolean;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

export interface CreateTeamRequest {
  name: string;
  description?: string;
}

export interface UpdateTeamRequest {
  name?: string;
  description?: string;
}
```

---

## Project Model

```typescript
// src/app/core/models/project.model.ts

export interface Project {
  _id: string;
  title: string;
  description?: string;
  teamId?: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

export interface CreateProjectRequest {
  title: string;
  description?: string;
  teamId?: string;
}

export interface UpdateProjectRequest {
  title?: string;
  description?: string;
  teamId?: string;
}
```

---

## Task Model

```typescript
// src/app/core/models/task.model.ts

export interface Task {
  _id: string;
  title: string;
  description?: string;
  status: TaskStatus;
  priority: TaskPriority;
  projectId: string;
  milestoneId?: string;
  assignTo?: string;
  lastAssignTo?: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

export enum TaskStatus {
  TODO = 'To Do',
  IN_PROGRESS = 'In Progress',
  IN_REVIEW = 'In Review',
  DONE = 'Done'
}

export enum TaskPriority {
  LOW = 'Low',
  MEDIUM = 'Medium',
  HIGH = 'High',
  CRITICAL = 'Critical'
}

export interface CreateTaskRequest {
  title: string;
  description?: string;
  status?: TaskStatus;
  priority?: TaskPriority;
  projectId: string;
  milestoneId?: string;
  assignTo?: string;
}

export interface UpdateTaskRequest {
  title?: string;
  description?: string;
  status?: TaskStatus;
  priority?: TaskPriority;
  milestoneId?: string;
  assignTo?: string;
}
```

---

## Milestone Model

```typescript
// src/app/core/models/milestone.model.ts

export interface Milestone {
  _id: string;
  name: string;
  projectId: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

export interface CreateMilestoneRequest {
  name: string;
  projectId: string;
}

export interface UpdateMilestoneRequest {
  name?: string;
}
```

---

## Event Model

```typescript
// src/app/core/models/event.model.ts

export interface Event {
  _id: string;
  title: string;
  description?: string;
  entityType: EntityType;
  entityId: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

export enum EntityType {
  USER = 'User',
  TEAM = 'Team',
  TASK = 'Task',
  PROJECT = 'Project',
  MILESTONE = 'Milestone'
}
```

---

## Pagination Model

```typescript
// src/app/core/models/pagination.model.ts

export interface PaginatedResult<T> {
  data: T[];
  pagination: PaginationMeta;
}

export interface PaginationMeta {
  page: number;
  limit: number;
  total: number;
  totalPages: number;
}

export interface PaginationParams {
  page: number;
  limit: number;
}
```

---

## API Response Model

```typescript
// src/app/core/models/api-response.model.ts

export interface ApiResponse<T> {
  status: 'success' | 'error';
  data: T;
  message?: string;
  token?: string;
}

export interface ApiError {
  status: 'error';
  message: string;
  errors?: Array<{
    field: string;
    message: string;
  }>;
}
```
