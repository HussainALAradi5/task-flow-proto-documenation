# Comment Model

## Location
`src/models/project/Comment.ts`

## Schema (Inherits BaseModel)

```typescript
const commentSchema = new Schema<IComment>({
  ...baseSchemaFields,
  content: { type: String, required: true },
  taskId: { type: Schema.Types.ObjectId, ref: 'Task', required: true },
}, { timestamps: true });
```

## Fields

| Field | Type | Required | Ref |
|-------|------|----------|-----|
| code | String | Yes | Unique identifier |
| createdBy | ObjectId | No | User |
| updatedBy | ObjectId | No | User |
| content | String | Yes | - |
| taskId | ObjectId | Yes | Task |
