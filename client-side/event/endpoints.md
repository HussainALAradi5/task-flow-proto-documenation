# Event Endpoints (Client)

## API Mapping

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getEvents` | GET | `/events?page=&limit=` | - |
| `getEvent` | GET | `/events/:id` | - |
| `createEvent` | POST | `/events` | `{ title, description?, entityType, entityId }` |
| `updateEvent` | PATCH | `/events/:id` | `{ title?, description? }` |
| `deleteEvent` | DELETE | `/events/:id` | - |
