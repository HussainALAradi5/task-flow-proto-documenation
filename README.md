# TaskFlow Proto

A Trello-like task management application built with the MEAN stack (MongoDB, Express.js, Angular, Node.js).

## Live demo

Use the [TaskFlow client](https://taskflow-proto-client.onrender.com) to test the app. The [API health endpoint](https://taskflow-proto-api.onrender.com/) shows whether the free server is awake; the first request after inactivity may take about a minute. The dedicated Atlas Free database has the [three seeded roles](#demo-seed). Ask the project owner for the shared demo password; the Admin credential is not published in Git. Setup details are in the [free deployment guide](deploy-free-render.md).

## Overview

TaskFlow Proto enables teams to organize projects into boards, tasks, and milestones with role-based access control. Inspired by Trello's simplicity, it provides a clean interface for managing workflows across teams.

See the [Trello-style workflow review](trello-workflow-review.md) for implemented collaboration, invitation, discussion, date rules, and remaining limits.

The current UI includes team chat, team boards, owner-only team management, team-specific leader/member badges, grid/list views, project scope filters, and an inbox with read/unread notifications. Use the bell in the header to open the inbox. The profile badge is the account role; a user can lead one team and join another as a team member. Sign in with email, username, or mobile, with email shown first in the form.

## Tech Stack

| Layer | Technology | Version |
|-------|-----------|---------|
| Frontend | Angular | 21.2.25 |
| CSS | Tailwind CSS | 4.3.3 |
| Backend | Express.js | 5.2.1 |
| Runtime | Node.js LTS | TypeScript 7.0.2 on the server |
| Database | MongoDB + Mongoose | 9.9.1 |
| Auth | JWT (jsonwebtoken) | 9.0.3 |
| Validation | Zod | 4.6.7 |

## Project Structure

```
task-flow-proto/
├── task-flow-proto-client-side/   # Angular frontend
├── task-flow-proto-server-side/   # Express.js backend
└── task-flow-proto-documenation/  # Project documentation (this repo)
```

## Documentation

See [client and server contract verification](contract-verification.md) for the routes used by the current UI, permission checks, and remaining runtime verification.

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
| Notification | [model and service](server-side/notification/model.md) | [model and service](server-side/notification/model.md) | [endpoints](server-side/notification/endpoints.md) | - | [model and service](server-side/notification/model.md) |

### Client-Side (Angular)

Each entity has service, model, and endpoints documentation.

| Entity | Service | Model | Endpoints |
|--------|---------|-------|-----------|
| [User](client-side/user/service.md) | Auth, profile management | TypeScript interfaces | API mapping |
| [Team](client-side/team/service.md) | CRUD operations | TypeScript interfaces | API mapping |
| [Project](client-side/project/service.md) | CRUD operations | TypeScript interfaces | API mapping |
| [Task](client-side/task/service.md) | CRUD + filtering | TypeScript interfaces | API mapping |
| [Milestone](client-side/milestone/service.md) | CRUD operations | TypeScript interfaces | API mapping |
| [Comment](client-side/comment/service.md) | List, create, delete | TypeScript interfaces | API mapping |
| [Event](client-side/event/service.md) | Board activity history | TypeScript interface | Paginated project history |
| [Notification](client-side/notification/service.md) | Inbox and unread count | Separate interface and enum | Recipient-scoped API |

## Collections

| File | Description |
|------|-------------|
| `TaskFlowProto.insomnia_export.json` | Insomnia collection for API testing |

## Quick Start

To put a demo online using free hosting, follow the [Render and MongoDB Atlas deployment guide](deploy-free-render.md).

Keep the [client](https://github.com/HussainALAradi5/task-flow-proto-client-side), [server](https://github.com/HussainALAradi5/task-flow-proto-server-side), and this documentation repository side by side. Use Node.js 24 LTS and a reachable MongoDB instance. From the server repository, create `.env` from `.env.example` and set `MONGO_URI` and a unique `JWT_SECRET`. Keep port 5000 and the client origin at `http://localhost:4200` for the default development configuration.

```powershell
# Terminal 1, from the server repository
npm ci
Copy-Item .env.example .env
# Edit .env, then start the API.
npm run dev

# Terminal 2, from the client repository
npm ci
npm start
```

### Demo seed

From the server repository, set `DEMO_SEED=1` and a unique `DEMO_SEED_PASSWORD` of at least 12 characters, then run `npm run seed:demo`. The seed reads `MONGO_URI` from `.env`. Use a dedicated demo database. Existing account passwords are preserved.

| Login email | Role | Group and access |
| --- | --- | --- |
| `demo-admin@taskflow.local` | Admin | Owns Operations Group; can see all boards |
| `demo@taskflow.local` | Leader | Owns Product Studio and its three boards |
| `demo-member@taskflow.local` | Member | Belongs to Operations Group and its Operations Board; cannot see Product Studio boards |

The Operations Board has an Admin-created card so the Member can try moving and commenting on another user's card. Website Refresh has four cards, a milestone, a comment, and ordered activity history. New notifications appear as people invite members, post team messages, or change boards; the seed does not pre-mark notifications read.

### Verification and screenshots

Run `npm run build` and `npm test` in each application repository. The client [screenshot gallery](https://github.com/HussainALAradi5/task-flow-proto-client-side#screenshots) shows all three roles against a live client/API and isolated temporary MongoDB instance. The seed ran twice successfully; Admin, Leader, and Member logins, board visibility, Member card movement, comments, and activity history passed. Invitation acceptance, role protection, date rejection, a GIF comment, and access revocation also passed against an isolated database. The configured Atlas demo database was seeded and its deployed API checked separately.

### Access rules

All API paths have the `/api` prefix. Signup and login are public. A new Member may create a project and is promoted to Leader. Project and team reads allow owners, explicit members, or Admin. Only a team creator can edit, delete, invite, or remove members. Accepted members and the creator can use team chat. Board members can work on cards and comments on their board. Team invitations are accepted or declined in the recipient's account. Card comments and team messages can contain a small verified image or GIF. Events are read-only to clients; notifications are private to their recipient and can be marked read. Media creation is not exposed; media listing is scoped to its creator. See each endpoint page for paths and validation.

## License

ISC
