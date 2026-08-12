# BaseService

## Location
`src/services/BaseService.ts`

## Function Signatures

```typescript
class BaseService<T extends mongoose.Document> {
  protected model: Model<T>;

  constructor(model: Model<T>);

  async create(data: Partial<T>): Promise<T>;
  async getById(id: string): Promise<T | null>;
  async getAll(filter?: QueryFilter<T>): Promise<T[]>;
  async getAllPaginated(filter: QueryFilter<T>, params: PaginationParams): Promise<PaginatedResult<T>>;
  async update(id: string, data: UpdateQuery<T>): Promise<T | null>;
  async softDelete(id: string): Promise<T | null>;
}
```

## Business Logic

| Method | Logic |
|--------|-------|
| `create` | Insert new document, return saved entity |
| `getById` | Find by MongoDB ObjectId |
| `getAll` | Find with optional filter (no pagination) |
| `getAllPaginated` | Find with pagination using `PaginationParams` |
| `update` | Find by ID and update, returns updated document |
| `softDelete` | Set `isActive: false` (no actual deletion) |

## Validation

Handled by `PaginationParams` interface:

```typescript
interface PaginationParams {
  page: number;   // min: 1, default: 1
  limit: number;  // min: 1, max: 100, default: 10
  skip: number;   // calculated: (page - 1) * limit
}
```

## Response

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
