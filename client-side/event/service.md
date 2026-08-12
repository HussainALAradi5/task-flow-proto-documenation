# Event Service (Client)

## Location
`src/app/features/board/board.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `getEvents` | `(page, limit): Observable<PaginatedResult<Event>>` | Get events |
| `getEvent` | `(id): Observable<Event>` | Get event by ID |
| `createEvent` | `(data): Observable<Event>` | Create event |
| `updateEvent` | `(id, data): Observable<Event>` | Update event |
| `deleteEvent` | `(id): Observable<void>` | Delete event |
