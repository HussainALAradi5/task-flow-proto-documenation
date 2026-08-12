# Team Endpoints (Client)

## API Mapping

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getTeams` | GET | `/teams?page=&limit=` | - |
| `getTeam` | GET | `/teams/:id` | - |
| `createTeam` | POST | `/teams` | `{ name, description? }` |
| `updateTeam` | PATCH | `/teams/:id` | `{ name?, description? }` |
| `deleteTeam` | DELETE | `/teams/:id` | - |
