# Task Enums

## GenericStatus

### Location
`src/enums/GenericStatus.ts`

```typescript
export enum GenericStatus {
  TODO = 'To Do',
  IN_PROGRESS = 'In Progress',
  IN_REVIEW = 'In Review',
  DONE = 'Done',
}
```

| Key | Value | Description |
|-----|-------|-------------|
| TODO | `To Do` | Task not started |
| IN_PROGRESS | `In Progress` | Task in progress |
| IN_REVIEW | `In Review` | Task under review |
| DONE | `Done` | Task completed |

## TaskPriority

### Location
`src/enums/project/TaskPriority.ts`

```typescript
export enum TaskPriority {
  LOW = 'Low',
  MEDIUM = 'Medium',
  HIGH = 'High',
  CRITICAL = 'Critical',
}
```

| Key | Value | Description |
|-----|-------|-------------|
| LOW | `Low` | Low priority |
| MEDIUM | `Medium` | Medium priority (default) |
| HIGH | `High` | High priority |
| CRITICAL | `Critical` | Critical priority |
