# Milestone Endpoints

## Protected (Auth Required)

| Method | Endpoint | Roles | Body | Description |
|--------|----------|-------|------|-------------|
| `POST` | `/milestones` | Admin, Leader | `{ name, projectId }` | Create milestone |
| `GET` | `/milestones` | All | - | List user's milestones |
| `GET` | `/milestones/project/:projectId` | All | - | Get milestones by project |
| `GET` | `/milestones/:id` | All | - | Get milestone by ID |
| `PATCH` | `/milestones/:id` | Admin, Leader | `{ name? }` | Update milestone |
| `DELETE` | `/milestones/:id` | Admin, Leader | - | Soft delete milestone |

## Security Rules
- Admin and Leader can create/update/delete milestones
- Users see only milestones they created (Admin sees all)
