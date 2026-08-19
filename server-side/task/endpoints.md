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
- `GET /tasks` - users see only tasks they created (Admin sees all)
- `GET /tasks/project/:projectId` - users see only their tasks in project (Admin sees all)
- `GET /tasks/milestone/:milestoneId` - users see only their tasks in milestone (Admin sees all)
- `GET /tasks/:id` - any authenticated user can view any task by ID
