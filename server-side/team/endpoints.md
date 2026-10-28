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
| `POST` | `/teams/:id/messages` | Creator or accepted member | `createTeamMessageSchema` | Add text, one verified file, and selected team mentions |

## Security Rules

- Admin and Leader can create teams
- `GET /teams` - users see teams they own or belong to (Admin sees all)
- `GET /teams/:id` - creator, explicit member, or Admin
- Only the team creator can edit, delete, invite, or remove members, even when another user has the Admin role. Missing and forbidden teams return 404.
- Invitations require an existing active account. Only the recipient can answer. Accepting adds access to the team and its active boards; declining does not change membership.
- Team chat requires accepted membership or ownership. Admin users outside a team cannot read or post. `content` is limited to 2,000 characters; optional `attachment` is a base64 data URL for one verified PNG, JPEG, GIF, WebP, PDF, or UTF-8 plain-text file up to 500 KB. Optional `attachmentName` must be a safe basename with the matching extension. The file remains in the protected MongoDB message document; no Render filesystem or external storage account is used.
- `mentions` is an array of at most 20 User ObjectIds. Every ID must belong to the current team, refer to an active account, and appear in `content` as `@userName`. The sender cannot choose notification recipients outside the team. Mentioned members receive a specific mention notification; the other participants receive the ordinary message notification.
- Invalid request fields return 400. Inaccessible teams return 404. `GET` returns paginated messages with populated authors and attachment data only after team access is checked.
