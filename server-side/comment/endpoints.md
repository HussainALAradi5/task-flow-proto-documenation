# Comment Endpoints

## Location
`src/routes/project/commentRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/comments` | Admin, Leader | `createCommentSchema` | Create comment |
| `GET` | `/comments/task/:taskId` | All | - | Get comments by task |
| `PATCH` | `/comments/:id` | All (ownership check) | `updateCommentSchema` | Update comment |
| `DELETE` | `/comments/:id` | All (ownership check) | - | Soft delete comment |

## Security Rules

- Admin and Leader can create comments
- Any authenticated user can view comments on a task
- Creator can edit their own comments
- Admin or Leader can edit any comment
- Creator can soft delete their own comments
- Admin or Leader can soft delete any comment
- Ownership checked in controller (not middleware)
