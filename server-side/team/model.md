# Team Model

## Location
`src/models/team/Team.ts`

## Schema (Inherits BaseModel)

```typescript
const teamSchema = new Schema<ITeam>({
  ...baseSchemaFields,
  name: { type: String, required: true },
  description: { type: String, default: '' },
  members: [{ type: Schema.Types.ObjectId, ref: 'User' }],
  isActive: { type: Boolean, default: true },
}, { timestamps: true });
```

## Fields

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| code | String | Yes | - | Unique identifier |
| createdBy | ObjectId | No | `null` | Ref → User |
| updatedBy | ObjectId | No | `null` | Ref → User |
| name | String | Yes | - | Team name |
| description | String | No | `""` | Description |
| members | ObjectId[] | No | `[]` | Explicit User members who can read the team |
| isActive | Boolean | No | `true` | Soft delete flag |

## Team message

`src/models/team/TeamMessage.ts` stores `teamId` and `author` as User/Team references, text `content`, optional base64 data-URL `attachment`, optional safe `attachmentName`, `mentions` as User ObjectIds, and timestamps. The model indexes `(teamId, createdAt, _id)` for newest-first pagination. Existing messages without the newer optional fields remain readable; no migration is required. The API checks team membership before returning the message or attachment data.
