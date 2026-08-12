# Project Service

## Location
`src/services/project/ProjectService.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `createProject` | `(data: Partial<IProject>): Promise<IProject>` | Create project + auto-promote creator to Leader |
| `update` | `(id, data): Promise<IProject \| null>` | Update project, log event |
| `softDelete` | `(id): Promise<IProject \| null>` | Deactivate project, log event |

## Business Logic
- Creator auto-promoted from Member to Leader
- Event logged on: create, update, deactivate
