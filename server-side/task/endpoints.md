# Task Endpoints

## Protected (Auth Required)

| Method | Endpoint | Roles | Body | Description |
|--------|----------|-------|------|-------------|
| `POST` | `/tasks` | Admin, Leader | `{ title, description?, status?, priority?, projectId, milestoneId?, assignTo? }` | Create task |
| `GET` | `/tasks` | All | - | List user's tasks |
| `GET` | `/tasks/project/:projectId` | All | - | Get tasks by project |
| `GET` | `/tasks/milestone/:milestoneId` | All | - | Get tasks by milestone |
| `GET` | `/tasks/:id` | All | - | Get task by ID |
| `PATCH` | `/tasks/:id` | Admin, Leader | `{ title?, description?, status?, priority?, milestoneId?, assignTo? }` | Update task |
| `DELETE` | `/tasks/:id` | Admin, Leader | - | Soft delete task |

## Security Rules
- Admin and Leader can create/update/delete tasks
- Users see only tasks they created (Admin sees all)
- Filter by project or milestone supported
