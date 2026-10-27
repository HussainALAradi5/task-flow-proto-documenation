# Task Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAllPages('tasks/project/' + projectId)` | GET | `/api/tasks/project/:projectId?page=&limit=` | - |
| `create('tasks', data)` | POST | `/api/tasks` | `{ title, description?, status?, priority?, projectId, milestoneId?, dates? }` |
| `update('tasks', id, data)` | PATCH | `/api/tasks/:id` | Task fields, status, priority, milestone, dates |
| `delete('tasks', id)` | DELETE | `/api/tasks/:id` | - |

Date fields are `startDate`, `targetDate`, `endDate`, and `deliveredDate`, each `YYYY-MM-DD` or `null`. The form checks chronological order and the API enforces it for every write.
