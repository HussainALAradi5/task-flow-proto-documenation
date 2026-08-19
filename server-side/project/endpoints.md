# Project Endpoints

## Location
`src/routes/project/projectRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/projects` | Admin, Leader | `createProjectSchema` | Create project |
| `GET` | `/projects` | All | - | List user's projects |
| `GET` | `/projects/:id` | All | - | Get project by ID |
| `PATCH` | `/projects/:id` | Admin, Leader | `updateProjectSchema` | Update project |
| `DELETE` | `/projects/:id` | Admin | - | Soft delete project |

## Security Rules

- Admin and Leader can create projects
- `GET /projects` - users see only projects they created (Admin sees all)
- `GET /projects/:id` - any authenticated user can view any project by ID
- `PATCH /projects/:id` - Admin and Leader only
- Only Admin can delete projects
- Creating a project auto-promotes Member to Leader
