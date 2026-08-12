# Task Model

## Location
`src/models/project/Task.ts`

## Schema (Inherits BaseModel)

```typescript
const taskSchema = new Schema<ITask>({
  ...baseSchemaFields,
  title: { type: String, required: true },
  description: { type: String, default: '' },
  status: { type: String, enum: Object.values(GenericStatus), default: GenericStatus.TODO },
  priority: { type: String, enum: Object.values(TaskPriority), default: TaskPriority.MEDIUM },
  projectId: { type: Schema.Types.ObjectId, ref: 'Project', required: true },
  milestoneId: { type: Schema.Types.ObjectId, ref: 'Milestone', default: null },
  assignTo: { type: Schema.Types.ObjectId, ref: 'User', default: null },
  lastAssignTo: { type: Schema.Types.ObjectId, ref: 'User', default: null },
}, { timestamps: true });
```

## Fields

| Field | Type | Required | Default | Ref |
|-------|------|----------|---------|-----|
| code | String | Yes | - | Unique identifier |
| createdBy | ObjectId | No | `null` | User |
| updatedBy | ObjectId | No | `null` | User |
| title | String | Yes | - | - |
| description | String | No | `""` | - |
| status | String | No | `To Do` | - |
| priority | String | No | `Medium` | - |
| projectId | ObjectId | Yes | - | Project |
| milestoneId | ObjectId | No | `null` | Milestone |
| assignTo | ObjectId | No | `null` | User |
| lastAssignTo | ObjectId | No | `null` | User |
