# Team Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAll('teams')` | GET | `/api/teams?page=&limit=` | - |
| `create('teams', data)` | POST | `/api/teams` | `{ name, description? }` |
| `update('teams', id, data)` | PATCH | `/api/teams/:id` | `{ name?, description? }` |
| `delete('teams', id)` | DELETE | `/api/teams/:id` | - |
