# Task Model

## Location
`src/models/project/Task.ts`

## Schema

| Field | Type | Required | Default | Ref |
|-------|------|----------|---------|-----|
| title | String | Yes | - | - |
| description | String | No | `""` | - |
| status | String | No | `To Do` | - |
| priority | String | No | `Medium` | - |
| projectId | ObjectId | Yes | - | Project |
| milestoneId | ObjectId | No | `null` | Milestone |
| assignTo | ObjectId | No | `null` | User |
| lastAssignTo | ObjectId | No | `null` | User |

## Enums
```typescript
enum GenericStatus {
  TODO = 'To Do',
  IN_PROGRESS = 'In Progress',
  IN_REVIEW = 'In Review',
  DONE = 'Done'
}

enum TaskPriority {
  LOW = 'Low',
  MEDIUM = 'Medium',
  HIGH = 'High',
  CRITICAL = 'Critical'
}
```
