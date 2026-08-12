# Client-Side Services

## Overview

Angular services handle API communication, state management, and business logic on the client side.

## Planned Structure

```
src/app/core/
├── auth/
│   └── auth.service.ts          # Login, signup, token management
├── interceptors/
│   └── auth.interceptor.ts      # JWT token injection
└── guards/
    └── auth.guard.ts            # Route protection

src/app/features/
├── auth/
│   └── auth.service.ts          # Auth-specific logic
├── board/
│   └── board.service.ts         # Board/task operations
├── team/
│   └── team.service.ts          # Team operations
└── settings/
    └── settings.service.ts      # User settings
```

---

## AuthService

**Location:** `src/app/core/auth/auth.service.ts`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `signup` | `(data: SignupRequest): Observable<AuthResponse>` | Register new user |
| `login` | `(data: LoginRequest): Observable<AuthResponse>` | Authenticate user |
| `getProfile` | `(): Observable<User>` | Get current user |
| `logout` | `(): void` | Clear token, navigate to login |
| `getToken` | `(): string \| null` | Get stored JWT |
| `isLoggedIn` | `(): boolean` | Check if authenticated |

### Business Logic

- Store JWT in localStorage
- Auto-attach token to requests via interceptor
- Redirect to login on 401

---

## BoardService

**Location:** `src/app/features/board/board.service.ts`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getProjects` | `(page, limit): Observable<PaginatedResult<Project>>` | Get user's projects |
| `getProject` | `(id): Observable<Project>` | Get project by ID |
| `createProject` | `(data): Observable<Project>` | Create project |
| `updateProject` | `(id, data): Observable<Project>` | Update project |
| `deleteProject` | `(id): Observable<void>` | Delete project |
| `getTasks` | `(projectId, page, limit): Observable<PaginatedResult<Task>>` | Get project tasks |
| `createTask` | `(data): Observable<Task>` | Create task |
| `updateTask` | `(id, data): Observable<Task>` | Update task |
| `deleteTask` | `(id): Observable<void>` | Delete task |

---

## TeamService

**Location:** `src/app/features/team/team.service.ts`

### Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getTeams` | `(page, limit): Observable<PaginatedResult<Team>>` | Get user's teams |
| `getTeam` | `(id): Observable<Team>` | Get team by ID |
| `createTeam` | `(data): Observable<Team>` | Create team |
| `updateTeam` | `(id, data): Observable<Team>` | Update team |
| `deleteTeam` | `(id): Observable<void>` | Delete team |

---

## Models

**Location:** `src/app/core/models/`

```typescript
interface User {
  _id: string;
  userName: string;
  email: string;
  mobileNumber?: string;
  teamId?: string;
  role: 'Admin' | 'Leader' | 'Member';
  isActive: boolean;
}

interface Team {
  _id: string;
  name: string;
  description?: string;
  isActive: boolean;
}

interface Project {
  _id: string;
  title: string;
  description?: string;
  teamId?: string;
}

interface Task {
  _id: string;
  title: string;
  description?: string;
  status: 'To Do' | 'In Progress' | 'In Review' | 'Done';
  priority: 'Low' | 'Medium' | 'High' | 'Critical';
  projectId: string;
  milestoneId?: string;
  assignTo?: string;
}

interface Milestone {
  _id: string;
  name: string;
  projectId: string;
}

interface PaginatedResult<T> {
  data: T[];
  pagination: {
    page: number;
    limit: number;
    total: number;
    totalPages: number;
  };
}
```
