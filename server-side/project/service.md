# Project Service

## Location
`src/services/project/ProjectService.ts`

## Function Signatures

```typescript
class ProjectServiceClass extends BaseService<IProject> {
  constructor();
  async createProject(data: Partial<IProject>): Promise<IProject>;
  async update(id: string, data: Partial<IProject>): Promise<IProject | null>;
  async softDelete(id: string): Promise<IProject | null>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `createProject` | Create project, auto-promote creator to Leader, log event "Project created" |
| `update` | Update project, log event "Project updated" |
| `softDelete` | Set isActive: false, log event "Project deactivated" |

## Validation

Handled by Zod schemas in `src/validations/project.schema.ts`:

```typescript
createProjectSchema = { body: { title: string(1-200), description?: string, teamId?: string } }
updateProjectSchema = { body: { title?: string(1-200), description?: string, teamId?: string }, params: { id: string } }
```
