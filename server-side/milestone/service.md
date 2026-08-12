# Milestone Service

## Location
`src/services/project/MilestoneService.ts`

## Function Signatures

```typescript
class MilestoneServiceClass extends BaseService<IMilestone> {
  constructor();
  async create(data: Partial<IMilestone>): Promise<IMilestone>;
  async update(id: string, data: Partial<IMilestone>): Promise<IMilestone | null>;
  async softDelete(id: string): Promise<IMilestone | null>;
  buildProjectFilter(projectId: string): QueryFilter<IMilestone>;
  buildProjectUserFilter(projectId: string, userId: string): QueryFilter<IMilestone>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `create` | Create milestone, log event "Milestone created" |
| `update` | Update milestone, log event "Milestone updated" |
| `softDelete` | Set isActive: false, log event "Milestone deactivated" |
| `buildProjectFilter` | Build query filter by projectId |
| `buildProjectUserFilter` | Build query filter by projectId + createdBy |

## Validation

Handled by Zod schemas in `src/validations/milestone.schema.ts`:

```typescript
createMilestoneSchema = { body: { name: string(1-200), projectId: string } }
updateMilestoneSchema = { body: { name?: string(1-200) }, params: { id: string } }
```
