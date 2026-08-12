# Milestone Service

## Location
`src/services/project/MilestoneService.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<IMilestone>): Promise<IMilestone>` | Create milestone, log event |
| `update` | `(id, data): Promise<IMilestone \| null>` | Update milestone, log event |
| `softDelete` | `(id): Promise<IMilestone \| null>` | Deactivate milestone, log event |
| `buildProjectFilter` | `(projectId): QueryFilter<IMilestone>` | Filter by project |
| `buildProjectUserFilter` | `(projectId, userId): QueryFilter<IMilestone>` | Filter by project + creator |
