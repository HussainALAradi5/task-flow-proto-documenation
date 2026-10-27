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
| `POST` | `/teams/:id/members` | Admin, Leader owner | `teamMemberSchema` | Send account invitation by email |
| `DELETE` | `/teams/:id/members/:userId` | Admin, Leader owner | `removeTeamMemberSchema` | Remove member from team and team boards |
| `GET` | `/teams/invitations/pending` | Recipient | - | List pending invitations in own account |
| `POST` | `/teams/invitations/:invitationId/respond` | Recipient | `respondToInvitationSchema` | Accept or decline |

## Security Rules

- Admin and Leader can create teams
- `GET /teams` - users see teams they own or belong to (Admin sees all)
- `GET /teams/:id` - creator, explicit member, or Admin
- `PATCH /teams/:id` - Admin or Leader, and the creator for non-Admins
- Only Admin can delete teams
- Invitations require an existing active account. Only the recipient can answer. Accepting adds access to the team and its active boards; declining does not change membership.
