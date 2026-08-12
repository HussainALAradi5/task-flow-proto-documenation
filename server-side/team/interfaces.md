# Team Interface

## Location
`src/interface/team/Team.ts`

## Interface

```typescript
import { IBaseEntity } from '../BaseModel';

export interface ITeam extends IBaseEntity {
  name: string;
  description?: string;
  isActive: boolean;
}
```

## Inherits From
- `IBaseEntity` (id, code, createdBy, updatedBy, createdAt, updatedAt)
