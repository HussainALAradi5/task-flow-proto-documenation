# Project Endpoints

## Location
`src/routes/project/projectRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/projects` | All signed-in users | `createProjectSchema` | Create project; Member creator becomes Leader |
| `GET` | `/projects` | All | - | List user's projects |
| `GET` | `/projects/:id` | All | - | Get project by ID |
| `GET` | `/projects/slug/:slug` | Owner, member, or Admin | - | Get active project by slug |
| `PATCH` | `/projects/:id` | Admin, Leader | `updateProjectSchema` | Update project |
| `DELETE` | `/projects/:id` | Admin | - | Soft delete project |

## Security Rules

- Any signed-in user can create a project. A Member creator is promoted to Leader.
- `GET /projects` - users see boards they own or are explicit members of (Admin sees all)
- `GET /projects/:id` - owner, explicit member, or Admin
- `PATCH /projects/:id` - Admin or Leader, and the creator for non-Admins
- `DELETE /projects/:id` - Admin only
- A supplied `teamId` must identify a team owned by the caller (or any team for Admin).
- Creating a project auto-promotes Member to Leader. When a project is created inside a team, the team members are copied into the board membership.
