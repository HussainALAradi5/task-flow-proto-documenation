# Team Interface

## Location
`src/interface/team/Team.ts`

## Interface

```typescript
import { IBaseEntity } from '../BaseModel';
import { Schema } from 'mongoose';

export interface ITeam extends IBaseEntity {
  name: string;
  description?: string;
  members: Schema.Types.ObjectId[];
  isActive: boolean;
}
```

## Inherits From
- `IBaseEntity` (id, code, createdBy, updatedBy, createdAt, updatedAt)
