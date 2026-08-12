# Milestone Model

## Location
`src/models/project/Milestone.ts`

## Schema (Inherits BaseModel)

```typescript
const milestoneSchema = new Schema<IMilestone>({
  ...baseSchemaFields,
  name: { type: String, required: true },
  projectId: { type: Schema.Types.ObjectId, ref: 'Project', required: true },
}, { timestamps: true });
```

## Fields

| Field | Type | Required | Ref |
|-------|------|----------|-----|
| code | String | Yes | Unique identifier |
| createdBy | ObjectId | No | User |
| updatedBy | ObjectId | No | User |
| name | String | Yes | - |
| projectId | ObjectId | Yes | Project |
