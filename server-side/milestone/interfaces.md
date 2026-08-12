# Milestone Interface

## Location
`src/interface/project/Milestone.ts`

## Interface

```typescript
import { Schema } from 'mongoose';
import { IBaseEntity } from '../BaseModel';

export interface IMilestone extends IBaseEntity {
  name: string;
  projectId: Schema.Types.ObjectId;
}
```

## Inherits From
- `IBaseEntity` (id, code, createdBy, updatedBy, createdAt, updatedAt)
