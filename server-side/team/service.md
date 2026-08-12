# Team Service

## Location
`src/services/team/TeamService.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<ITeam>): Promise<ITeam>` | Create team, log event |
| `update` | `(id, data): Promise<ITeam \| null>` | Update team, log event |
| `softDelete` | `(id): Promise<ITeam \| null>` | Deactivate team, log event |

## Business Logic
- Event logged on: create, update, deactivate
- Inherits: getAll, getById, getAllPaginated from BaseService
