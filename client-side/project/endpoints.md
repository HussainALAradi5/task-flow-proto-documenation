# Project Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAll('projects')` | GET | `/api/projects?page=&limit=` | - |
| `getById('projects/slug', slug)` | GET | `/api/projects/slug/:slug` | - |
| `create('projects', data)` | POST | `/api/projects` | `{ title, description? }` |
| `update('projects', id, data)` | PATCH | `/api/projects/:id` | `{ title?, description? }` |
| `delete('projects', id)` | DELETE | `/api/projects/:id` | - |
