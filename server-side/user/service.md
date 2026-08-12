# User Service

## Location
`src/services/user/UserService.ts`

## Function Signatures

```typescript
class UserServiceClass extends BaseService<IUser> {
  constructor();
  async create(data: Partial<IUser>): Promise<IUser>;
  async update(id: string, data: Partial<IUser>): Promise<IUser | null>;
  async authenticate(email: string, passwordPlain: string): Promise<IUser | null>;
  async findByEmailOrUsername(email: string, userName: string): Promise<IUser | null>;
  async assignRole(userId: string, role: UserRole): Promise<IUser | null>;
  async promoteToLeaderForNewProject(userId: string): Promise<IUser | null>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `create` | Hash password (bcrypt, 10 rounds), assign default Member role, log event |
| `update` | Update user fields, log event |
| `authenticate` | Find by email (select +password), compare with bcrypt, return user or null |
| `findByEmailOrUsername` | Check if email or username already exists ($or query) |
| `assignRole` | Update user role, log event |
| `promoteToLeaderForNewProject` | If user is Member, promote to Leader |

## Validation

Handled by Zod schemas in `src/validations/user.schema.ts`:

```typescript
signupSchema = { body: { userName: string(3-50), email: email, password: string(min 6), mobileNumber?: string } }
loginSchema = { body: { email: email, password: string(min 1) } }
updateUserSchema = { body: { userName?: string(3-50), email?: email, mobileNumber?: string, teamId?: string }, params: { id: string } }
updateRoleSchema = { body: { role: 'Admin' | 'Leader' | 'Member' }, params: { id: string } }
```
