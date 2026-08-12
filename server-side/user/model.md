# User Model

## Location
`src/models/user/User.ts`

## Schema (Inherits BaseModel)

```typescript
const userSchema = new Schema<IUser>({
  ...baseSchemaFields,
  userName: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  mobileNumber: { type: String, default: '' },
  teamId: { type: Schema.Types.ObjectId, ref: 'Team', default: null },
  role: createMongooseEnum(UserRole, UserRole.MEMBER),
  isActive: { type: Boolean, default: true },
}, { timestamps: true });
```

## Fields

| Field | Type | Required | Unique | Default | Ref |
|-------|------|----------|--------|---------|-----|
| code | String | Yes | Yes | - | - |
| createdBy | ObjectId | No | No | `null` | User |
| updatedBy | ObjectId | No | No | `null` | User |
| userName | String | Yes | Yes | - | - |
| password | String | Yes | No | - | - |
| email | String | Yes | Yes | - | - |
| mobileNumber | String | No | No | `""` | - |
| teamId | ObjectId | No | No | `null` | Team |
| role | String | No | No | `Member` | - |
| isActive | Boolean | No | No | `true` | - |

## Indexes
- `userName` (unique)
- `email` (unique)
