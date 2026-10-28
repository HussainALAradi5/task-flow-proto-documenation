# Team Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAll('teams')` | GET | `/api/teams?page=&limit=` | - |
| `create('teams', data)` | POST | `/api/teams` | `{ name, description? }` |
| `update('teams', id, data)` | PATCH | `/api/teams/:id` | `{ name?, description? }` |
| `delete('teams', id)` | DELETE | `/api/teams/:id` | - |
| `addMember(id, email)` | POST | `/api/teams/:id/members` | `{ email }` creates invitation |
| `pendingInvitations()` | GET | `/api/teams/invitations/pending` | - |
| `respondToInvitation(id, decision)` | POST | `/api/teams/invitations/:id/respond` | `{ decision: 'accept' \| 'decline' }` |
| `removeMember(id, userId)` | DELETE | `/api/teams/:id/members/:userId` | - |
| `getMessages(teamId, page)` | GET | `/api/teams/:id/messages?page=&limit=50` | - |
| `sendMessage(teamId, body)` | POST | `/api/teams/:id/messages` | `SendTeamMessageRequest` with `content`, `mentions`, optional `attachment` data URL and `attachmentName` |
