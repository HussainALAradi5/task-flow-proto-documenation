# Team Model (Client)

## Location
`src/app/core/models/team.model.ts`

## Interface
```typescript
interface Team {
  _id: string;
  name: string;
  description?: string;
  isActive: boolean;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

interface CreateTeamRequest {
  name: string;
  description?: string;
}

interface UpdateTeamRequest {
  name?: string;
  description?: string;
}
```
