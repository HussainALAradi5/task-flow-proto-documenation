# Project Endpoints

## Location
`src/routes/project/projectRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/projects` | All signed-in users | `createProjectSchema` | Create project; Member creator becomes Leader |
| `GET` | `/projects?scope=all|my|team&teamId=:id&page=&limit=` | All | Query values checked in controller | Paginated accessible projects; filter by owner, team projects, or one team |
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
- A supplied `teamId` must identify an active team owned by the caller or one where the caller is an accepted member. Admin role alone does not grant permission to place a board in another team's workspace.
- Creating a project auto-promotes Member to Leader. When a project is created inside a team, the team members are copied into the board membership.
- Project list responses populate the team's name for the colored team badge. `scope=my` filters by project creator; `scope=team` filters to projects with a team. All scopes retain the normal board access filter.
