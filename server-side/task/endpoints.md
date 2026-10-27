# Task Endpoints

## Location
`src/routes/project/taskRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/tasks` | All | `createTaskSchema` | Create task in an accessible board |
| `GET` | `/tasks` | All | - | List user's tasks |
| `GET` | `/tasks/project/:projectId` | All | - | Get tasks by project |
| `GET` | `/tasks/milestone/:milestoneId` | All | - | Get tasks by milestone |
| `GET` | `/tasks/:id` | All | - | Get task by ID |
| `PATCH` | `/tasks/:id` | Board owner/member or Admin | `updateTaskSchema` | Update task |
| `DELETE` | `/tasks/:id` | Board owner/member or Admin | - | Soft delete task |

## Security Rules

- A board owner, explicit board member, or Admin can create, update, move, and deactivate cards in that board. A status change records a `Task moved` activity event.
- `GET /tasks` - users see only tasks they created (Admin sees all)
- `GET /tasks/project/:projectId` - board members see all cards in their board; outsiders receive 404
- `GET /tasks/milestone/:milestoneId` - board members see all cards in the milestone; outsiders receive 404
- `GET /tasks/:id` - creator or Admin only
- Task dates use `YYYY-MM-DD` or `null`. Start, target, end, and delivery must be in that order when present, and none may precede the task creation day. Updates validate the merged existing and incoming timeline; invalid changes return 400.
