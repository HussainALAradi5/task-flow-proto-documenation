# Project Interface

## Location
`src/interface/project/Project.ts`

## Interface

```typescript
import { Schema } from 'mongoose';
import { IBaseEntity } from '../BaseModel';

export interface IProject extends IBaseEntity {
  title: string;
  description?: string;
  teamId?: Schema.Types.ObjectId;
}
```

## Inherits From
- `IBaseEntity` (id, code, createdBy, updatedBy, createdAt, updatedAt)
