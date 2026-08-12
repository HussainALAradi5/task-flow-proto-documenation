# Task Service

## Location
`src/services/project/TaskService.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<ITask>): Promise<ITask>` | Create task, log event |
| `update` | `(id, data): Promise<ITask \| null>` | Update task, log event |
| `softDelete` | `(id): Promise<ITask \| null>` | Deactivate task, log event |
| `buildProjectFilter` | `(projectId): QueryFilter<ITask>` | Filter tasks by project |
| `buildProjectUserFilter` | `(projectId, userId): QueryFilter<ITask>` | Filter by project + creator |
| `buildMilestoneFilter` | `(milestoneId): QueryFilter<ITask>` | Filter tasks by milestone |
| `buildMilestoneUserFilter` | `(milestoneId, userId): QueryFilter<ITask>` | Filter by milestone + creator |

## Business Logic
- Filter builders for type-safe queries
- Event logged on: create, update, deactivate
