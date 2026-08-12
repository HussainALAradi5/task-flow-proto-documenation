# Event Model (Client)

## Location
`src/app/core/models/event.model.ts`

## Interface
```typescript
interface Event {
  _id: string;
  title: string;
  description?: string;
  entityType: EntityType;
  entityId: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

enum EntityType {
  USER = 'User',
  TEAM = 'Team',
  TASK = 'Task',
  PROJECT = 'Project',
  MILESTONE = 'Milestone'
}
```
