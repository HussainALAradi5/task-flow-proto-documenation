# Event Endpoints

## Location
`src/routes/eventRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/events` | Admin, Leader | `createEventSchema` | Create event |
| `GET` | `/events` | All | - | List events |
| `GET` | `/events/:id` | All | - | Get event by ID |
| `PATCH` | `/events/:id` | Admin | `updateEventSchema` | Update event |
| `DELETE` | `/events/:id` | Admin | - | Delete event |

## Security Rules

- Admin and Leader can create events
- Users see only events they created (Admin sees all)
- Only Admin can update/delete events
