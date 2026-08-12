# User Model

## Location
`src/models/user/User.ts`

## Schema

| Field | Type | Required | Unique | Default | Ref |
|-------|------|----------|--------|---------|-----|
| userName | String | Yes | Yes | - | - |
| password | String | Yes | No | - | - |
| email | String | Yes | Yes | - | - |
| mobileNumber | String | No | No | `""` | - |
| teamId | ObjectId | No | No | `null` | Team |
| role | String | No | No | `Member` | - |
| isActive | Boolean | No | No | `true` | - |

## Enum
```typescript
enum UserRole {
  ADMIN = 'Admin',
  LEADER = 'Leader',
  MEMBER = 'Member'
}
```
