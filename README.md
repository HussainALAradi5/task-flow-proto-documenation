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

Each entity has 5 documentation files: model, service, endpoints, enums, interfaces.

| Entity | Model | Service | Endpoints | Enums | Interfaces |
|--------|-------|---------|-----------|-------|------------|
| BaseModel | [model](server-side/base-model/model.md) | [service](server-side/base-model/service.md) | - | - | [interfaces](server-side/base-model/interfaces.md) |
| User | [model](server-side/user/model.md) | [service](server-side/user/service.md) | [endpoints](server-side/user/endpoints.md) | [enums](server-side/user/enums.md) | [interfaces](server-side/user/interfaces.md) |
| Team | [model](server-side/team/model.md) | [service](server-side/team/service.md) | [endpoints](server-side/team/endpoints.md) | [enums](server-side/team/enums.md) | [interfaces](server-side/team/interfaces.md) |
| Project | [model](server-side/project/model.md) | [service](server-side/project/service.md) | [endpoints](server-side/project/endpoints.md) | [enums](server-side/project/enums.md) | [interfaces](server-side/project/interfaces.md) |
| Task | [model](server-side/task/model.md) | [service](server-side/task/service.md) | [endpoints](server-side/task/endpoints.md) | [enums](server-side/task/enums.md) | [interfaces](server-side/task/interfaces.md) |
| Milestone | [model](server-side/milestone/model.md) | [service](server-side/milestone/service.md) | [endpoints](server-side/milestone/endpoints.md) | [enums](server-side/milestone/enums.md) | [interfaces](server-side/milestone/interfaces.md) |
| Comment | [model](server-side/comment/model.md) | [service](server-side/comment/service.md) | [endpoints](server-side/comment/endpoints.md) | [enums](server-side/comment/enums.md) | [interfaces](server-side/comment/interfaces.md) |
| Event | [model](server-side/event/model.md) | [service](server-side/event/service.md) | [endpoints](server-side/event/endpoints.md) | [enums](server-side/event/enums.md) | [interfaces](server-side/event/interfaces.md) |

### Client-Side (Angular)

Each entity has service, model, and endpoints documentation.

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
