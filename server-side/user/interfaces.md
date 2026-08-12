# User Interface

## Location
`src/interface/user/User.ts`

## Interface

```typescript
import { Schema } from 'mongoose';
import { IBaseEntity } from '../BaseModel';
import { UserRole } from '../../enums/user/UserRole';

export interface IUser extends IBaseEntity {
  userName: string;
  password?: string;
  email: string;
  mobileNumber?: string;
  teamId?: Schema.Types.ObjectId;
  role: UserRole;
  isActive: boolean;
}
```

## Inherits From
- `IBaseEntity` (id, code, createdBy, updatedBy, createdAt, updatedAt)
