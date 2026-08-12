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

| Document | Description |
|----------|-------------|
| [Architecture](ARCHITECTURE.md) | Folder structure, code patterns, conventions |
| [Authentication](AUTH.md) | JWT flow, signup, login, token management |
| [Roles & Permissions](ROLES.md) | Role-based access control matrix |
| [API Reference](API.md) | REST API endpoints, request/response schemas |
| [Data Models](MODELS.md) | MongoDB schemas, relationships, enums |
| [Setup Guide](SETUP.md) | Installation, configuration, running locally |
| [Changelog](CHANGELOG.md) | Version history |

## Quick Start

See [SETUP.md](SETUP.md) for detailed installation instructions.

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
