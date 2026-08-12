# Team Service

## Location
`src/services/team/TeamService.ts`

## Function Signatures

```typescript
class TeamServiceClass extends BaseService<ITeam> {
  constructor();
  async create(data: Partial<ITeam>): Promise<ITeam>;
  async update(id: string, data: Partial<ITeam>): Promise<ITeam | null>;
  async softDelete(id: string): Promise<ITeam | null>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `create` | Create team, log event "Team created" |
| `update` | Update team, log event "Team updated" |
| `softDelete` | Set isActive: false, log event "Team deactivated" |

## Validation

Handled by Zod schemas in `src/validations/team.schema.ts`:

```typescript
createTeamSchema = { body: { name: string(1-100), description?: string } }
updateTeamSchema = { body: { name?: string(1-100), description?: string }, params: { id: string } }
```
