# User Enums

## Location
`src/enums/user/UserRole.ts`

## UserRole

```typescript
export enum UserRole {
  ADMIN = 'Admin',
  LEADER = 'Leader',
  MEMBER = 'Member',
}
```

## Values

| Key | Value | Description |
|-----|-------|-------------|
| ADMIN | `Admin` | Full system access, bypasses all restrictions |
| LEADER | `Leader` | Can manage team projects/tasks |
| MEMBER | `Member` | Default role; may create a project and then becomes Leader. Task access is scoped to records created by the user. |

## Default
- New users get `MEMBER` on signup
- Auto-promoted to `LEADER` when creating a project
