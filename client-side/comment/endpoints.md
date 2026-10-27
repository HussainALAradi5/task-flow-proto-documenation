# Comment Endpoints (Client)

## API Mapping

| UI call through ApiService | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getAllPages('comments/task/' + taskId)` | GET | `/api/comments/task/:taskId?page=&limit=` | - |
| `create('comments', data)` | POST | `/api/comments` | `{ content, taskId, attachment? }`; attachment is a validated image/GIF data URL |
| `delete('comments', id)` | DELETE | `/api/comments/:id` | - |
