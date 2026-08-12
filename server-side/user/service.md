# User Service

## Location
`src/services/user/UserService.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<IUser>): Promise<IUser>` | Hash password, assign default Member role, log event |
| `update` | `(id, data): Promise<IUser \| null>` | Update user, log event |
| `authenticate` | `(email, password): Promise<IUser \| null>` | Verify credentials with bcrypt |
| `findByEmailOrUsername` | `(email, userName): Promise<IUser \| null>` | Check uniqueness |
| `assignRole` | `(userId, role): Promise<IUser \| null>` | Admin-only role change, log event |
| `promoteToLeaderForNewProject` | `(userId): Promise<IUser \| null>` | Auto-promote Member to Leader |

## Business Logic
- Passwords hashed with bcrypt (10 salt rounds)
- Default role: `Member`
- Auto-promotion to `Leader` on project creation
- Event logged on: create, update, role change
