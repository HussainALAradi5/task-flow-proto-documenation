# Client-Side Endpoints

## Overview

Angular HTTP service configuration and API endpoint mapping.

## Environment Configuration

```typescript
// src/environments/environment.ts
export const environment = {
  production: false,
  apiUrl: 'http://localhost:5000/api'
};
```

## HTTP Interceptor

**Location:** `src/app/core/interceptors/auth.interceptor.ts`

```typescript
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const token = localStorage.getItem('token');
    if (token) {
      req = req.clone({
        setHeaders: { Authorization: `Bearer ${token}` }
      });
    }
    return next.handle(req);
  }
}
```

## API Endpoints Used

### Auth

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `signup` | POST | `/users/signup` | `{ userName, email, password, mobileNumber? }` |
| `login` | POST | `/users/login` | `{ email, password }` |
| `getProfile` | GET | `/users/profile` | - |

### Users

| Service Method | HTTP | Endpoint | Body/Params |
|----------------|------|----------|-------------|
| `getUsers` | GET | `/users?page=&limit=` | - |
| `getUser` | GET | `/users/:id` | - |
| `updateUser` | PATCH | `/users/:id` | `{ userName?, email?, mobileNumber? }` |
| `updateRole` | PATCH | `/users/:id/role` | `{ role }` |
| `deleteUser` | DELETE | `/users/:id` | - |

### Teams

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getTeams` | GET | `/teams?page=&limit=` | - |
| `getTeam` | GET | `/teams/:id` | - |
| `createTeam` | POST | `/teams` | `{ name, description? }` |
| `updateTeam` | PATCH | `/teams/:id` | `{ name?, description? }` |
| `deleteTeam` | DELETE | `/teams/:id` | - |

### Projects

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getProjects` | GET | `/projects?page=&limit=` | - |
| `getProject` | GET | `/projects/:id` | - |
| `createProject` | POST | `/projects` | `{ title, description?, teamId? }` |
| `updateProject` | PATCH | `/projects/:id` | `{ title?, description?, teamId? }` |
| `deleteProject` | DELETE | `/projects/:id` | - |

### Tasks

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getTasks` | GET | `/tasks?page=&limit=` | - |
| `getTasksByProject` | GET | `/tasks/project/:projectId?page=&limit=` | - |
| `getTasksByMilestone` | GET | `/tasks/milestone/:milestoneId?page=&limit=` | - |
| `getTask` | GET | `/tasks/:id` | - |
| `createTask` | POST | `/tasks` | `{ title, description?, status?, priority?, projectId, milestoneId?, assignTo? }` |
| `updateTask` | PATCH | `/tasks/:id` | `{ title?, description?, status?, priority?, milestoneId?, assignTo? }` |
| `deleteTask` | DELETE | `/tasks/:id` | - |

### Milestones

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getMilestones` | GET | `/milestones/project/:projectId?page=&limit=` | - |
| `getMilestone` | GET | `/milestones/:id` | - |
| `createMilestone` | POST | `/milestones` | `{ name, projectId }` |
| `updateMilestone` | PATCH | `/milestones/:id` | `{ name? }` |
| `deleteMilestone` | DELETE | `/milestones/:id` | - |

### Events

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getEvents` | GET | `/events?page=&limit=` | - |
| `getEvent` | GET | `/events/:id` | - |
| `createEvent` | POST | `/events` | `{ title, description?, entityType, entityId }` |
| `updateEvent` | PATCH | `/events/:id` | `{ title?, description? }` |
| `deleteEvent` | DELETE | `/events/:id` | - |

## Error Handling

```typescript
// Shared error handler
@Injectable()
export class ErrorHandler {
  handleError(error: HttpErrorResponse): Observable<never> {
    if (error.status === 401) {
      this.authService.logout();
      this.router.navigate(['/login']);
    }
    return throwError(() => error.error);
  }
}
```
