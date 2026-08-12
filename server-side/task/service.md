# Task Service

## Location
`src/services/project/TaskService.ts`

## Function Signatures

```typescript
class TaskServiceClass extends BaseService<ITask> {
  constructor();
  async create(data: Partial<ITask>): Promise<ITask>;
  async update(id: string, data: Partial<ITask>): Promise<ITask | null>;
  async softDelete(id: string): Promise<ITask | null>;
  buildProjectFilter(projectId: string): QueryFilter<ITask>;
  buildProjectUserFilter(projectId: string, userId: string): QueryFilter<ITask>;
  buildMilestoneFilter(milestoneId: string): QueryFilter<ITask>;
  buildMilestoneUserFilter(milestoneId: string, userId: string): QueryFilter<ITask>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `create` | Create task, log event "Task created" |
| `update` | Update task, log event "Task updated" |
| `softDelete` | Set isActive: false, log event "Task deactivated" |
| `buildProjectFilter` | Build query filter by projectId |
| `buildProjectUserFilter` | Build query filter by projectId + createdBy |
| `buildMilestoneFilter` | Build query filter by milestoneId |
| `buildMilestoneUserFilter` | Build query filter by milestoneId + createdBy |

## Validation

Handled by Zod schemas in `src/validations/task.schema.ts`:

```typescript
createTaskSchema = { body: {
  title: string(1-200),
  description?: string,
  status?: 'To Do' | 'In Progress' | 'In Review' | 'Done',
  priority?: 'Low' | 'Medium' | 'High' | 'Critical',
  projectId: string,
  milestoneId?: string,
  assignTo?: string
}}
updateTaskSchema = { body: {
  title?: string(1-200),
  description?: string,
  status?: 'To Do' | 'In Progress' | 'In Review' | 'Done',
  priority?: 'Low' | 'Medium' | 'High' | 'Critical',
  milestoneId?: string,
  assignTo?: string
}, params: { id: string }}
```
