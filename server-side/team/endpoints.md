# Team Endpoints

## Location
`src/routes/team/teamRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/teams` | Admin, Leader | `createTeamSchema` | Create team |
| `GET` | `/teams` | All | - | List user's teams |
| `GET` | `/teams/:id` | All | - | Get team by ID |
| `PATCH` | `/teams/:id` | Admin, Leader | `updateTeamSchema` | Update team |
| `DELETE` | `/teams/:id` | Admin | - | Soft delete team |

## Security Rules

- Admin and Leader can create teams
- `GET /teams` - users see only teams they created (Admin sees all)
- `GET /teams/:id` - any authenticated user can view any team by ID
- `PATCH /teams/:id` - Admin and Leader only
- Only Admin can delete teams
