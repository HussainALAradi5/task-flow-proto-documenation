# Event Model

## Location
`src/models/Event.ts`

## Schema

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| title | String | Yes | Event title |
| description | String | No | Details |
| entityType | String | Yes | Entity type |
| entityId | ObjectId | Yes | Polymorphic ref |

## Enum
```typescript
enum EntityType {
  USER = 'User',
  TEAM = 'Team',
  TASK = 'Task',
  PROJECT = 'Project',
  MILESTONE = 'Milestone'
}
```
