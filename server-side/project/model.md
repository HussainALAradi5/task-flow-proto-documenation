# Project Model

## Location
`src/models/project/Project.ts`

## Schema (Inherits BaseModel)

```typescript
const projectSchema = new Schema<IProject>({
  ...baseSchemaFields,
  title: { type: String, required: true },
  description: { type: String, default: '' },
  teamId: { type: Schema.Types.ObjectId, ref: 'Team', default: null },
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
| teamId | ObjectId | No | `null` | Team |
