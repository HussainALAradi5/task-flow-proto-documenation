# Comment Service

## Location
`src/services/project/CommentService.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<IComment>): Promise<IComment>` | Create comment, log event |
| `update` | `(id, data): Promise<IComment \| null>` | Update comment, log event |
| `softDelete` | `(id): Promise<IComment \| null>` | Delete comment, log event |
| `buildTaskFilter` | `(taskId): QueryFilter<IComment>` | Filter by task |
| `buildTaskUserFilter` | `(taskId, userId): QueryFilter<IComment>` | Filter by task + creator |

## Business Logic
- Only comment owner or Admin can edit/delete
- Event logged on: create, update, delete
