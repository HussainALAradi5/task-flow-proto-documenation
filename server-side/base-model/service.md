# BaseService

## Location
`src/services/BaseService.ts`

## Generic CRUD Operations

All services extend this base class.

| Method | Signature | Description |
|--------|-----------|-------------|
| `create` | `(data: Partial<T>): Promise<T>` | Insert new document |
| `getById` | `(id: string): Promise<T \| null>` | Find by ID |
| `getAll` | `(filter?): Promise<T[]>` | Find all with filter |
| `getAllPaginated` | `(filter, params): Promise<PaginatedResult<T>>` | Paginated find |
| `update` | `(id, data): Promise<T \| null>` | Update document |
| `softDelete` | `(id): Promise<T \| null>` | Set `isActive: false` |

## Pagination

```typescript
interface PaginatedResult<T> {
  data: T[];
  pagination: {
    page: number;
    limit: number;
    total: number;
    totalPages: number;
  };
}
```

## Usage

```typescript
class MyService extends BaseService<IMyEntity> {
  constructor() {
    super(MyModel);
  }
  // Add custom methods
}
```
