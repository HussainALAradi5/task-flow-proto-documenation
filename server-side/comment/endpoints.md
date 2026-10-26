# Comment Endpoints

## Location
`src/routes/project/commentRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/comments` | Board owner/member or Admin | `createCommentSchema` | Create comment |
| `GET` | `/comments/task/:taskId` | All | - | Get comments by task |
| `PATCH` | `/comments/:id` | All (ownership check) | `updateCommentSchema` | Update comment |
| `DELETE` | `/comments/:id` | All (ownership check) | - | Soft delete comment |

## Security Rules

- A board owner, explicit board member, or Admin can create and view comments on cards in that board
- Creator can edit their own comments
- Admin can edit any comment
- Creator can soft delete their own comments
- Admin can soft delete any comment
- The controller also checks current board access before editing or deleting a comment.
