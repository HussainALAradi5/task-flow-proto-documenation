# Milestone Service (Client)

## Location
`src/app/features/board/board.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getMilestones` | `(projectId, page, limit): Observable<PaginatedResult<Milestone>>` | Get milestones by project |
| `getMilestone` | `(id): Observable<Milestone>` | Get milestone by ID |
| `createMilestone` | `(data): Observable<Milestone>` | Create milestone |
| `updateMilestone` | `(id, data): Observable<Milestone>` | Update milestone |
| `deleteMilestone` | `(id): Observable<void>` | Delete milestone |
