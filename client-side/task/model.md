# Task Model (Client)

## Location
`src/app/core/models/task.model.ts`

## Interface
```typescript
interface Task {
  _id: string;
  title: string;
  description?: string;
  status: TaskStatus;
  priority: TaskPriority;
  projectId: string;
  milestoneId?: string;
  assignTo?: string;
  lastAssignTo?: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

enum TaskStatus {
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

interface CreateTaskRequest {
  title: string;
  description?: string;
  status?: TaskStatus;
  priority?: TaskPriority;
  projectId: string;
  milestoneId?: string;
  assignTo?: string;
}

interface UpdateTaskRequest {
  title?: string;
  description?: string;
  status?: TaskStatus;
  priority?: TaskPriority;
  milestoneId?: string;
  assignTo?: string;
}
```
