# Team Model

## Location
`src/models/team/Team.ts`

## Schema (Inherits BaseModel)

```typescript
const teamSchema = new Schema<ITeam>({
  ...baseSchemaFields,
  name: { type: String, required: true },
  description: { type: String, default: '' },
  isActive: { type: Boolean, default: true },
}, { timestamps: true });
```

## Fields

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| code | String | Yes | - | Unique identifier |
| createdBy | ObjectId | No | `null` | Ref → User |
| updatedBy | ObjectId | No | `null` | Ref → User |
| name | String | Yes | - | Team name |
| description | String | No | `""` | Description |
| isActive | Boolean | No | `true` | Soft delete flag |
