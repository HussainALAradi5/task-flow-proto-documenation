# Comment Service (Client)

## Location
`src/app/features/board/board.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getCommentsByTask` | `(taskId, page, limit): Observable<PaginatedResult<Comment>>` | Get comments by task |
| `createComment` | `(data): Observable<Comment>` | Create comment |
| `updateComment` | `(id, data): Observable<Comment>` | Update comment |
| `deleteComment` | `(id): Observable<void>` | Delete comment |
