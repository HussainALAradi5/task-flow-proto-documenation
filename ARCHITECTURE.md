# Architecture

## Overview

TaskFlow Proto follows a **layered architecture** with clear separation of concerns. The backend uses an OOP inheritance pattern with generic base classes, while the frontend uses modern Angular standalone components with signals.

## Repository Structure

```
task-flow-proto/
├── task-flow-proto-client-side/       # Angular 21 frontend
│   ├── src/
│   │   ├── app/
│   │   │   ├── app.ts                 # Root component (standalone)
│   │   │   ├── app.config.ts          # Application configuration
│   │   │   └── app.routes.ts          # Route definitions
│   │   ├── index.html
│   │   ├── main.ts                    # Bootstrap entry
│   │   └── styles.css                 # Global styles (Tailwind)
│   ├── angular.json
│   ├── package.json
│   └── tsconfig.json
│
├── task-flow-proto-server-side/       # Express.js backend
│   ├── src/
│   │   ├── server.ts                  # Entry point
│   │   ├── app.ts                     # Express app setup
│   │   ├── config/                    # Environment & database config
│   │   ├── models/                    # Mongoose schemas
│   │   ├── interface/                 # TypeScript interfaces
│   │   ├── enums/                     # Enum definitions
│   │   ├── middlewares/               # Auth, error, 404 handlers
│   │   ├── controllers/               # Request handlers
│   │   ├── services/                  # Business logic
│   │   ├── routes/                    # Route definitions
│   │   └── utilities/                 # Helpers (catchAsync, enumUtils, validateRequest)
│   ├── package.json
│   └── tsconfig.json
│
└── task-flow-proto-documenation/      # Documentation (this repo)
    ├── README.md
    ├── ARCHITECTURE.md
    ├── AUTH.md
    ├── ROLES.md
    ├── API.md
    ├── MODELS.md
    ├── SETUP.md
    └── CHANGELOG.md
```

## Backend Architecture

### Inheritance Hierarchy

The server follows a strict **generic inheritance pattern**:

```
BaseModel (shared schema fields)
    └── User, Team, Project, Task, Milestone, Event

BaseService<T> (generic CRUD operations)
    ├── UserService
    ├── TeamService
    ├── ProjectService
    ├── TaskService
    ├── MilestoneService
    └── EventService

BaseController<T> (generic request handlers)
    ├── UserController
    ├── TeamController
    ├── ProjectController
    ├── TaskController
    ├── MilestoneController
    └── EventController

BaseRoute<T> (generic route setup)
    ├── UserRoute
    ├── TeamRoute
    ├── ProjectRoute
    ├── TaskRoute
    ├── MilestoneRoute
    └── EventRoute
```

### Layer Responsibilities

| Layer | Responsibility | Key Pattern |
|-------|---------------|-------------|
| **Routes** | Define HTTP endpoints, apply middleware | Extends `BaseRoute`, adds custom routes |
| **Controllers** | Handle request/response, input parsing | Extends `BaseController`, uses `catchAsync` |
| **Services** | Business logic, data access | Extends `BaseService`, Mongoose operations |
| **Models** | Schema definition, data structure | Extends `baseSchemaFields`, Mongoose `Schema` |
| **Interfaces** | TypeScript type contracts | Extends `IBaseEntity` |
| **Enums** | Constant values, type safety | String enums with display values |
| **Middlewares** | Cross-cutting concerns | Auth, validation, error handling |

### Singleton Pattern

All services, controllers, and routes are exported as **singleton instances**:

```typescript
// Service singleton
export const UserService = new UserServiceClass();

// Controller singleton
export const UserController = new UserControllerClass();

// Route singleton (returns router instance)
export default new UserRouteClass().router;
```

### Generic Base Classes

**BaseService<T>** provides:
- `create(data)` - Insert new document
- `getById(id)` - Find by ID
- `getAll(filter)` - Find with filter
- `update(id, data)` - Find and update
- `softDelete(id)` - Set `isActive: false`

**BaseController<T>** provides:
- `create` - Injects `createdBy` from authenticated user
- `getAll` - Scopes to user's records (admin bypass)
- `getById` - Standard lookup
- `update` - Standard update
- `delete` - Soft delete

**BaseRoute<T>** provides:
- `POST /` - Create
- `GET /` - Get all
- `GET /:id` - Get by ID
- `PATCH /:id` - Update
- `DELETE /:id` - Delete

### Error Handling

```
catchAsync (wraps async handlers)
    → next(error)
        → globalErrorHandler (formats response)
```

All async handlers are wrapped with `catchAsync` to prevent unhandled promise rejections.

### User Data Isolation

Non-admin users only see records they created (`createdBy` filter). Admins see all records:

```typescript
// BaseController.getAll
if (req.user && req.user.role !== UserRole.ADMIN) {
  filter.createdBy = req.user.id;
}
```

## Frontend Architecture

### Angular 21 Patterns

- **Standalone components** (no NgModules)
- **Signal-based state** (`signal()`, `computed()`)
- **New control flow** (`@for`, `@if`, `@switch`)
- **Tailwind CSS** for styling
- **Vitest** for testing

### Planned Structure

```
src/app/
├── core/                    # Singleton services, guards, interceptors
│   ├── auth/
│   ├── guards/
│   └── interceptors/
├── shared/                  # Reusable components, pipes, directives
├── features/                # Feature modules
│   ├── auth/
│   ├── board/
│   ├── team/
│   └── settings/
└── layout/                  # Layout components (header, sidebar)
```

## Code Conventions

### TypeScript

- Strict mode enabled
- No `any` types (use generics, unknown, or specific types)
- Interfaces for all data structures
- Enums for constant values

### Naming

| Item | Convention | Example |
|------|-----------|---------|
| Files | PascalCase for classes, camelCase for utilities | `UserService.ts`, `catchAsync.ts` |
| Classes | PascalCase | `BaseService`, `UserController` |
| Variables | camelCase | `userService`, `currentUser` |
| Enums | PascalCase enum, UPPER_SNAKE_CASE values | `UserRole.ADMIN` |
| Routes | camelCase | `userRoutes`, `projectRoutes` |
| Interfaces | PascalCase with `I` prefix | `IUser`, `IBaseEntity` |

### File Organization

Each domain entity follows the same folder structure:

```
src/
├── models/user/User.ts          # Mongoose schema
├── interface/user/User.ts       # TypeScript interface
├── enums/user/UserRoleEnum.ts   # Enums
├── services/user/UserService.ts # Business logic
├── controllers/user/UserController.ts # Request handlers
└── routes/user/userRoutes.ts    # Route definitions
```

### Response Format

All API responses follow a consistent structure:

```json
{
  "status": "success | error",
  "data": {},
  "message": "Optional message",
  "token": "JWT token (auth responses only)"
}
```

### Middleware Order

```
1. express.json()        → Body parsing
2. cors()                → Cross-origin
3. Router                → Route matching
   ├── Public routes     → No auth required
   └── protect           → JWT verification
       └── restrictTo    → Role authorization
4. notFoundHandler       → 404 for unmatched routes
5. globalErrorHandler    → Catch all errors
```
