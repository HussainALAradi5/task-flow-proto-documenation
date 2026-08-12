# Comment Model (Client)

## Location
`src/app/core/models/comment.model.ts`

## Interface
```typescript
interface Comment {
  _id: string;
  content: string;
  taskId: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

interface CreateCommentRequest {
  content: string;
  taskId: string;
}

interface UpdateCommentRequest {
  content: string;
}
```
