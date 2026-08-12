# User Model (Client)

## Location
`src/app/core/models/user.model.ts`

## Interface
```typescript
interface User {
  _id: string;
  userName: string;
  email: string;
  mobileNumber?: string;
  teamId?: string;
  role: 'Admin' | 'Leader' | 'Member';
  isActive: boolean;
  createdAt: string;
  updatedAt: string;
}

enum UserRole {
  ADMIN = 'Admin',
  LEADER = 'Leader',
  MEMBER = 'Member'
}
```
