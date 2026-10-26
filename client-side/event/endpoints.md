# Event endpoints used by the client

| Method | Path | Request | Response |
| --- | --- | --- | --- |
| GET | `/api/events/project/:projectId` | `page` and `limit` query parameters; bearer token | `{ status: 'success', data: ActivityEvent[], pagination }` |

A user outside the board receives 404. Clients cannot create, update, or delete activity events directly.
