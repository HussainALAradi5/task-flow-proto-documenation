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
| MEMBER | `Member` | Default role, view/edit assigned tasks only |

## Default
- New users get `MEMBER` on signup
- Auto-promoted to `LEADER` when creating a project
