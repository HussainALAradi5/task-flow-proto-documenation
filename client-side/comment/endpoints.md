# Comment Endpoints (Client)

## API Mapping

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getCommentsByTask` | GET | `/comments/task/:taskId?page=&limit=` | - |
| `createComment` | POST | `/comments` | `{ content, taskId }` |
| `updateComment` | PATCH | `/comments/:id` | `{ content }` |
| `deleteComment` | DELETE | `/comments/:id` | - |
