# Comment Endpoints

## Location
`src/routes/project/commentRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/comments` | Admin, Leader | `createCommentSchema` | Create comment |
| `GET` | `/comments/task/:taskId` | All | - | Get comments by task |
| `PATCH` | `/comments/:id` | Owner, Admin | `updateCommentSchema` | Update comment |
| `DELETE` | `/comments/:id` | Owner, Admin | - | Soft delete comment |

## Security Rules

- Admin and Leader can create comments
- Users can only edit/delete their own comments
- Admin can edit/delete any comment
- Ownership checked in controller
