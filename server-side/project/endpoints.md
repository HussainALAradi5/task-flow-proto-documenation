# Project Endpoints

## Protected (Auth Required)

| Method | Endpoint | Roles | Body | Description |
|--------|----------|-------|------|-------------|
| `POST` | `/projects` | Admin, Leader | `{ title, description?, teamId? }` | Create project |
| `GET` | `/projects` | All | - | List user's projects |
| `GET` | `/projects/:id` | All | - | Get project by ID |
| `PATCH` | `/projects/:id` | Admin, Leader | `{ title?, description?, teamId? }` | Update project |
| `DELETE` | `/projects/:id` | Admin | - | Soft delete project |

## Security Rules
- Admin and Leader can create projects
- Users see only projects they created (Admin sees all)
- Only Admin can delete projects
- Creating a project auto-promotes Member to Leader
