# Comment Interface

## Location
`src/interface/project/Comment.ts`

## Interface

```typescript
import { Schema } from 'mongoose';
import { IBaseEntity } from '../BaseModel';

export interface IComment extends IBaseEntity {
  content: string;
  taskId: Schema.Types.ObjectId;
}
```

## Inherits From
- `IBaseEntity` (id, code, createdBy, updatedBy, createdAt, updatedAt)
