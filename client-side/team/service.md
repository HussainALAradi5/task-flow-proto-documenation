# Team Service (Client)

## Location
`src/app/features/team/team.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getTeams` | `(page, limit): Observable<PaginatedResult<Team>>` | Get user's teams |
| `getTeam` | `(id): Observable<Team>` | Get team by ID |
| `createTeam` | `(data): Observable<Team>` | Create team |
| `updateTeam` | `(id, data): Observable<Team>` | Update team |
| `deleteTeam` | `(id): Observable<void>` | Delete team |
