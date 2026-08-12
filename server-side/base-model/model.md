# BaseModel

## Location
`src/models/BaseModel.ts`

## Schema

```typescript
export const baseSchemaFields = {
  code: { type: String, required: true, unique: true },
  createdBy: { type: Schema.Types.ObjectId, ref: 'User', default: null },
  updatedBy: { type: Schema.Types.ObjectId, ref: 'User', default: null },
};
```

## Fields

| Field | Type | Required | Unique | Default | Ref |
|-------|------|----------|--------|---------|-----|
| code | String | Yes | Yes | - | - |
| createdBy | ObjectId | No | No | `null` | User |
| updatedBy | ObjectId | No | No | `null` | User |

## Usage

All models spread this into their schema:

```typescript
const mySchema = new Schema<IMyEntity>({
  ...baseSchemaFields,
  // entity-specific fields
});
```
