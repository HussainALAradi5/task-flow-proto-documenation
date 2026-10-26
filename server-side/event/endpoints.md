# Event Endpoints

Location: `src/routes/eventRoutes.ts`. All paths have the `/api` prefix and require authentication.

| Method | Path | Access | Response |
|--------|------|--------|----------|
| GET | `/events` | Creator's events; Admin sees all | Paginated events |
| GET | `/events/:id` | Creator or Admin | Event or 404 |
| GET | `/events/project/:projectId` | Board owner, explicit member, or Admin | Newest-first paginated board, card, milestone, and comment activity; 404 for outsiders |

Events are written by backend services when records change. The API does not accept event creation, updates, or deletion from clients, so callers cannot forge audit entries.
