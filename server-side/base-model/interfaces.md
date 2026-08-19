# BaseModel Interface

## Location
`src/interface/BaseModel.ts`

## Interface

```typescript
import { Types } from 'mongoose';
import * as mongoose from 'mongoose';

export interface IBaseEntity extends mongoose.Document {
  id: string;
  __v: number;
  code: string;
  createdBy?: Types.ObjectId;
  updatedBy?: Types.ObjectId;
  createdAt: Date;
  updatedAt: Date;
}
```

## Fields

| Field | Type | Description |
|-------|------|-------------|
| id | string | Document ID (auto-generated) |
| __v | number | Version key (auto-generated) |
| code | string | Unique identifier string |
| createdBy | Types.ObjectId | Ref → User (creator) |
| updatedBy | Types.ObjectId | Ref → User (last updater) |
| createdAt | Date | Creation timestamp |
| updatedAt | Date | Last update timestamp |

## Extended By
- `IUser`
- `ITeam`
- `IProject`
- `ITask`
- `IMilestone`
- `IComment`
- `IEvent`
