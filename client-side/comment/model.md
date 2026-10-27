# Comment Model (Client)

## Location
`src/app/core/interfaces/comment.interface.ts`

## Interface
```typescript
interface Comment {
  _id: string;
  content: string;
  attachment?: string;
  taskId: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

interface CreateCommentRequest {
  content: string;
  attachment?: string;
  taskId: string;
}

interface UpdateCommentRequest {
  content: string;
}
```
