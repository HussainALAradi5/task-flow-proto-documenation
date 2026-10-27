# Project Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAll(params, ..., scope, teamId)` | GET | `/api/projects?page=&limit=&scope=&teamId=` | - |
| `getById('projects/slug', slug)` | GET | `/api/projects/slug/:slug` | - |
| `create('projects', data)` | POST | `/api/projects` | `{ title, description?, teamId? }` |
| `update('projects', id, data)` | PATCH | `/api/projects/:id` | `{ title?, description?, teamId?: string \| null }` |
| `delete('projects', id)` | DELETE | `/api/projects/:id` | - |
