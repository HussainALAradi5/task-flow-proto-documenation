# Event Endpoints

## Protected (Auth Required)

| Method | Endpoint | Roles | Body | Description |
|--------|----------|-------|------|-------------|
| `POST` | `/events` | Admin, Leader | `{ title, description?, entityType, entityId }` | Create event |
| `GET` | `/events` | All | - | List events |
| `GET` | `/events/:id` | All | - | Get event by ID |
| `PATCH` | `/events/:id` | Admin | `{ title?, description? }` | Update event |
| `DELETE` | `/events/:id` | Admin | - | Delete event |

## Security Rules
- Admin and Leader can create events
- Users see only events they created (Admin sees all)
- Only Admin can update/delete events
