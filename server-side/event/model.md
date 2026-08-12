# Event Model

## Location
`src/models/Event.ts`

## Schema (Inherits BaseModel)

```typescript
const eventSchema = new Schema<IEvent>({
  ...baseSchemaFields,
  title: { type: String, required: true },
  description: { type: String, default: '' },
  entityType: createMongooseEnum(EntityType),
  entityId: { type: Schema.Types.ObjectId, required: true },
}, { timestamps: true });
```

## Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| code | String | Yes | Unique identifier |
| createdBy | ObjectId | No | Ref → User |
| updatedBy | ObjectId | No | Ref → User |
| title | String | Yes | Event title |
| description | String | No | Details |
| entityType | String | Yes | Entity type |
| entityId | ObjectId | Yes | Polymorphic ref |
