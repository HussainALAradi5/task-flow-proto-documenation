# Task Endpoints

## Location
`src/routes/project/taskRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/tasks` | Admin, Leader | `createTaskSchema` | Create task |
| `GET` | `/tasks` | All | - | List user's tasks |
| `GET` | `/tasks/project/:projectId` | All | - | Get tasks by project |
| `GET` | `/tasks/milestone/:milestoneId` | All | - | Get tasks by milestone |
| `GET` | `/tasks/:id` | All | - | Get task by ID |
| `PATCH` | `/tasks/:id` | Admin, Leader | `updateTaskSchema` | Update task |
| `DELETE` | `/tasks/:id` | Admin, Leader | - | Soft delete task |

## Security Rules

- Admin and Leader can create/update/delete tasks
- Users see only tasks they created (Admin sees all)
- Filter by project or milestone supported
