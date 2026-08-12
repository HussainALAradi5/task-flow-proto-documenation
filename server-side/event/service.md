# Event Service

## Location
`src/services/EventService.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `logEvent` | `(title, entityType, entityId, description?, userId?): Promise<IEvent>` | Create audit log entry |

## Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| title | string | Event title |
| entityType | EntityType | User, Team, Task, Project, Milestone |
| entityId | string | Related entity ID |
| description | string | Optional details |
| userId | string | User who triggered event |

## Auto-Logged Events
- `{Entity} created` on create
- `{Entity} updated` on update
- `{Entity} deactivated` on soft delete
- `User role updated` on role change
