# TaskFlow Proto

A Trello-like task management application built with the MEAN stack (MongoDB, Express.js, Angular, Node.js).

## Overview

TaskFlow Proto enables teams to organize projects into boards, tasks, and milestones with role-based access control. Inspired by Trello's simplicity, it provides a clean interface for managing workflows across teams.

## Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Frontend | Angular | 21.2.0 |
| CSS | Tailwind CSS | 4.1.12 |
| Backend | Express.js | 5.2.1 |
| Runtime | Node.js | TypeScript 7.0.2 |
| Database | MongoDB + Mongoose | 9.9.1 |
| Auth | JWT (jsonwebtoken) | 9.0.3 |
| Validation | Zod | 4.4.3 |

## Project Structure

```
task-flow-proto/
├── task-flow-proto-client-side/   # Angular frontend
├── task-flow-proto-server-side/   # Express.js backend
└── task-flow-proto-documenation/  # Project documentation (this repo)
```

## Documentation

### Server-Side (Express.js + MongoDB)

Each entity has its own folder with service, model, and endpoints documentation.

| Entity | Service | Model | Endpoints |
|--------|---------|-------|-----------|
| [BaseModel](server-side/base-model/service.md) | Generic CRUD, pagination | Schema fields, interface | - |
| [User](server-side/user/service.md) | Auth, roles, password hashing | Schema, enums | Signup, login, profile, CRUD |
| [Team](server-side/team/service.md) | CRUD with event logging | Schema | Create, list, update, delete |
| [Project](server-side/project/service.md) | CRUD + auto role promotion | Schema | Create, list, update, delete |
| [Task](server-side/task/service.md) | CRUD + filter builders | Schema, status/priority enums | CRUD by project/milestone |
| [Milestone](server-side/milestone/service.md) | CRUD with event logging | Schema | CRUD by project |
| [Comment](server-side/comment/service.md) | CRUD with ownership checks | Schema | CRUD by task |
| [Event](server-side/event/service.md) | Audit log helper | Schema, entity types | List, create, update |

### Client-Side (Angular)

Each entity has its own folder with service, model, and endpoints documentation.

| Entity | Service | Model | Endpoints |
|--------|---------|-------|-----------|
| [User](client-side/user/service.md) | Auth, profile management | TypeScript interfaces | API mapping |
| [Team](client-side/team/service.md) | CRUD operations | TypeScript interfaces | API mapping |
| [Project](client-side/project/service.md) | CRUD operations | TypeScript interfaces | API mapping |
| [Task](client-side/task/service.md) | CRUD + filtering | TypeScript interfaces | API mapping |
| [Milestone](client-side/milestone/service.md) | CRUD operations | TypeScript interfaces | API mapping |
| [Comment](client-side/comment/service.md) | CRUD operations | TypeScript interfaces | API mapping |
| [Event](client-side/event/service.md) | Audit log | TypeScript interfaces | API mapping |

## Collections

| File | Description |
|------|-------------|
| `TaskFlowProto.insomnia_export.json` | Insomnia collection for API testing |

## Quick Start

```bash
# Backend
cd task-flow-proto-server-side
npm install
npm run dev

# Frontend
cd task-flow-proto-client-side
npm install
npm start
```

## License

ISC
