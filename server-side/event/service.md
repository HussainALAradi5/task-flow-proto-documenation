# Event Service

## Location
`src/services/EventService.ts`

## Function Signatures

```typescript
class EventServiceClass extends BaseService<IEvent> {
  constructor();
  async logEvent(
    title: string,
    entityType: EntityType,
    entityId: string,
    description?: string,
    userId?: string
  ): Promise<IEvent>;
  async getProjectHistory(projectId: string, params: PaginationParams): Promise<PaginatedResult<IEvent>>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `logEvent` | Create audit log entry with entity reference and acting user |
| `getProjectHistory` | Collect project, task, and milestone events for one board; order by `createdAt` then `_id` descending and paginate |

## Auto-Logged Events

| Trigger | Event Title | EntityType |
|---------|-------------|------------|
| User created | `User created` | User |
| User updated | `User updated` | User |
| User role changed | `User role updated` | User |
| Team created | `Team created` | Team |
| Team updated | `Team updated` | Team |
| Team deactivated | `Team deactivated` | Team |
| Project created | `Project created` | Project |
| Project updated | `Project updated` | Project |
| Project deactivated | `Project deactivated` | Project |
| Task created | `Task created` | Task |
| Task updated | `Task updated` | Task |
| Task status changed | `Task moved` with old and new status | Task |
| Task deactivated | `Task deactivated` | Task |
| Milestone created | `Milestone created` | Milestone |
| Milestone updated | `Milestone updated` | Milestone |
| Milestone deactivated | `Milestone deactivated` | Milestone |
| Comment created | `Comment created` | Task |
| Comment updated | `Comment updated` | Task |
| Comment deleted | `Comment deleted` | Task |

## Write access

Only backend services call `logEvent`. The event API exposes GET routes and has no client write schema.
