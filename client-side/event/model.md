# Activity event model in the client

Location: `src/app/core/interfaces/event.interface.ts`.

`ActivityEvent` has `_id`, `title`, optional `description`, `entityType`, `entityId`, optional `createdBy` (user ID or populated user with `_id`, `userName`, `email`), and ISO `createdAt`. It is used by the activity panel on the project detail page. The response is wrapped in the standard `PaginatedResult<ActivityEvent>` envelope.
