# Project Service (Client)

## Location
`src/app/features/board/board.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getProjects` | `(page, limit): Observable<PaginatedResult<Project>>` | Get user's projects |
| `getProject` | `(id): Observable<Project>` | Get project by ID |
| `createProject` | `(data): Observable<Project>` | Create project |
| `updateProject` | `(id, data): Observable<Project>` | Update project |
| `deleteProject` | `(id): Observable<void>` | Delete project |
