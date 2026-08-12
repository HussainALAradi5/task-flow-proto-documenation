# Team Endpoints

## Protected (Auth Required)

| Method | Endpoint | Roles | Body | Description |
|--------|----------|-------|------|-------------|
| `POST` | `/teams` | Admin, Leader | `{ name, description? }` | Create team |
| `GET` | `/teams` | All | - | List user's teams |
| `GET` | `/teams/:id` | All | - | Get team by ID |
| `PATCH` | `/teams/:id` | Admin, Leader | `{ name?, description? }` | Update team |
| `DELETE` | `/teams/:id` | Admin | - | Soft delete team |

## Security Rules
- Admin and Leader can create teams
- Users see only teams they created (Admin sees all)
- Only Admin can delete teams
