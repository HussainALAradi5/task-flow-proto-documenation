# Task Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAllPages('tasks/project/' + projectId)` | GET | `/api/tasks/project/:projectId?page=&limit=` | - |
| `create('tasks', data)` | POST | `/api/tasks` | `{ title, description?, status?, priority?, projectId, milestoneId?, dates? }` |
| `update('tasks', id, data)` | PATCH | `/api/tasks/:id` | Task fields, status, priority, milestone, dates |
| `delete('tasks', id)` | DELETE | `/api/tasks/:id` | - |
