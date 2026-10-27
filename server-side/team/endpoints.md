# Team Endpoints

## Location
`src/routes/team/teamRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/teams` | Admin, Leader | `createTeamSchema` | Create team |
| `GET` | `/teams` | All | - | List user's teams |
| `GET` | `/teams/:id` | All | - | Get team by ID |
| `PATCH` | `/teams/:id` | Creator only | `updateTeamSchema` | Update team |
| `DELETE` | `/teams/:id` | Creator only | - | Soft delete team |
| `POST` | `/teams/:id/members` | Creator only | `teamMemberSchema` | Send account invitation by email |
| `DELETE` | `/teams/:id/members/:userId` | Creator only | `removeTeamMemberSchema` | Remove member from team and team boards |
| `GET` | `/teams/invitations/pending` | Recipient | - | List pending invitations in own account |
| `POST` | `/teams/invitations/:invitationId/respond` | Recipient | `respondToInvitationSchema` | Accept or decline |
| `GET` | `/teams/:id/messages?page=&limit=` | Creator or accepted member | `listTeamMessagesSchema` | Newest messages first, paginated |
| `POST` | `/teams/:id/messages` | Creator or accepted member | `createTeamMessageSchema` | Add text and/or one verified image or GIF up to 500 KB |

## Security Rules

- Admin and Leader can create teams
- `GET /teams` - users see teams they own or belong to (Admin sees all)
- `GET /teams/:id` - creator, explicit member, or Admin
- Only the team creator can edit, delete, invite, or remove members, even when another user has the Admin role. Missing and forbidden teams return 404.
- Invitations require an existing active account. Only the recipient can answer. Accepting adds access to the team and its active boards; declining does not change membership.
- Team chat requires accepted membership or ownership. Admin users outside a team cannot read or post. Messages contain text up to 2,000 characters and/or one verified PNG, JPEG, GIF, or WebP data image up to 500 KB. A message notifies the other team participants.
