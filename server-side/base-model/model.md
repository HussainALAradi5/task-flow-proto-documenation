# BaseModel

## Location
`src/models/BaseModel.ts`

## Schema Fields

Every model includes these base fields:

| Field | Type | Required | Unique | Default | Description |
|-------|------|----------|--------|---------|-------------|
| code | String | Yes | Yes | - | Unique identifier string |
| createdBy | ObjectId | No | No | `null` | Ref → User (creator) |
| updatedBy | ObjectId | No | No | `null` | Ref → User (last updater) |

## Usage

```typescript
import { baseSchemaFields } from '../BaseModel';

const mySchema = new Schema<IMyEntity>({
  ...baseSchemaFields,
  // entity-specific fields
});
```

## Interface

```typescript
// src/interface/BaseModel.ts
interface IBaseEntity extends mongoose.Document {
  id: string;
  __v: number;
  code: string;
  createdBy?: Types.ObjectId;
  updatedBy?: Types.ObjectId;
  createdAt: Date;
  updatedAt: Date;
}
```
