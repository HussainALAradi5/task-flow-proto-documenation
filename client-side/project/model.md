# Project Model (Client)

## Location
`src/app/core/models/project.model.ts`

## Interface
```typescript
interface Project {
  _id: string;
  title: string;
  description?: string;
  teamId?: string;
  createdBy?: string;
  createdAt: string;
  updatedAt: string;
}

interface CreateProjectRequest {
  title: string;
  description?: string;
  teamId?: string;
}

interface UpdateProjectRequest {
  title?: string;
  description?: string;
  teamId?: string;
}
```
