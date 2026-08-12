# Comment Service

## Location
`src/services/project/CommentService.ts`

## Function Signatures

```typescript
class CommentServiceClass extends BaseService<IComment> {
  constructor();
  async create(data: Partial<IComment>): Promise<IComment>;
  async update(id: string, data: Partial<IComment>): Promise<IComment | null>;
  async softDelete(id: string): Promise<IComment | null>;
  buildTaskFilter(taskId: string): QueryFilter<IComment>;
  buildTaskUserFilter(taskId: string, userId: string): QueryFilter<IComment>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `create` | Create comment, log event on parent task |
| `update` | Update comment, log event on parent task |
| `softDelete` | Set isActive: false, log event on parent task |
| `buildTaskFilter` | Build query filter by taskId |
| `buildTaskUserFilter` | Build query filter by taskId + createdBy |

## Validation

Handled by Zod schemas in `src/validations/comment.schema.ts`:

```typescript
createCommentSchema = { body: { content: string(1-2000), taskId: string } }
updateCommentSchema = { body: { content: string(1-2000) }, params: { id: string } }
```
