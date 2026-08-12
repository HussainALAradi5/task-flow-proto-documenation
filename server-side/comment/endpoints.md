# Comment Endpoints

## Protected (Auth Required)

| Method | Endpoint | Roles | Body | Description |
|--------|----------|-------|------|-------------|
| `POST` | `/comments` | Admin, Leader | `{ content, taskId }` | Create comment |
| `GET` | `/comments/task/:taskId` | All | - | Get comments by task |
| `PATCH` | `/comments/:id` | Owner, Admin | `{ content }` | Update comment |
| `DELETE` | `/comments/:id` | Owner, Admin | - | Soft delete comment |

## Security Rules
- Admin and Leader can create comments
- Users can only edit/delete their own comments
- Admin can edit/delete any comment
