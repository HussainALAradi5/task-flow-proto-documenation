# Milestone Model (Client)

## Location
`src/app/core/models/milestone.model.ts`

## Interface
```typescript
interface Milestone {
  _id: string;
  name: string;
  projectId: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

interface CreateMilestoneRequest {
  name: string;
  projectId: string;
}

interface UpdateMilestoneRequest {
  name?: string;
}
```
