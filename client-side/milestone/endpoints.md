# Milestone Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAllPages('milestones/project/' + projectId)` | GET | `/api/milestones/project/:projectId?page=&limit=` | - |
| `create('milestones', data)` | POST | `/api/milestones` | `{ name, projectId }` |
| `update('milestones', id, data)` | PATCH | `/api/milestones/:id` | `{ name? }` |
| `delete('milestones', id)` | DELETE | `/api/milestones/:id` | - |
