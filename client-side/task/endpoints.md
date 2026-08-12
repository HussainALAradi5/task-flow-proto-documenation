# Task Endpoints (Client)

## API Mapping

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getTasks` | GET | `/tasks?page=&limit=` | - |
| `getTasksByProject` | GET | `/tasks/project/:projectId?page=&limit=` | - |
| `getTasksByMilestone` | GET | `/tasks/milestone/:milestoneId?page=&limit=` | - |
| `getTask` | GET | `/tasks/:id` | - |
| `createTask` | POST | `/tasks` | `{ title, description?, status?, priority?, projectId, milestoneId?, assignTo? }` |
| `updateTask` | PATCH | `/tasks/:id` | `{ title?, description?, status?, priority?, milestoneId?, assignTo? }` |
| `deleteTask` | DELETE | `/tasks/:id` | - |
