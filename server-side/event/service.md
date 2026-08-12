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
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `logEvent` | Create audit log entry with entity reference |

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
| Task deactivated | `Task deactivated` | Task |
| Milestone created | `Milestone created` | Milestone |
| Milestone updated | `Milestone updated` | Milestone |
| Milestone deactivated | `Milestone deactivated` | Milestone |
| Comment created | `Comment created` | Task |
| Comment updated | `Comment updated` | Task |
| Comment deleted | `Comment deleted` | Task |

## Validation

Handled by Zod schemas in `src/validations/event.schema.ts`:

```typescript
createEventSchema = { body: {
  title: string(1-200),
  description?: string,
  entityType: 'User' | 'Team' | 'Task' | 'Project' | 'Milestone',
  entityId: string
}}
updateEventSchema = { body: { title?: string(1-200), description?: string }, params: { id: string } }
```
