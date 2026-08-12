# Project Endpoints (Client)

## API Mapping

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getProjects` | GET | `/projects?page=&limit=` | - |
| `getProject` | GET | `/projects/:id` | - |
| `createProject` | POST | `/projects` | `{ title, description?, teamId? }` |
| `updateProject` | PATCH | `/projects/:id` | `{ title?, description?, teamId? }` |
| `deleteProject` | DELETE | `/projects/:id` | - |
