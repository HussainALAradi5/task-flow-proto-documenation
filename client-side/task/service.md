# Task Service (Client)

## Location
`src/app/features/board/board.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getTasks` | `(page, limit): Observable<PaginatedResult<Task>>` | Get user's tasks |
| `getTasksByProject` | `(projectId, page, limit): Observable<PaginatedResult<Task>>` | Get tasks by project |
| `getTasksByMilestone` | `(milestoneId, page, limit): Observable<PaginatedResult<Task>>` | Get tasks by milestone |
| `getTask` | `(id): Observable<Task>` | Get task by ID |
| `createTask` | `(data): Observable<Task>` | Create task |
| `updateTask` | `(id, data): Observable<Task>` | Update task |
| `deleteTask` | `(id): Observable<void>` | Delete task |
