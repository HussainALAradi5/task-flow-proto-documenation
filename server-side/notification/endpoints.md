# Notification endpoints

All paths use `/api` and require a valid JWT. Queries and mutations are restricted to the authenticated recipient. Another user's notification ID returns 404.

| Method and path | Request | Response | Controller and rule |
| --- | --- | --- | --- |
| `GET /notifications?page=&limit=&unread=true|false` | Optional page, limit, unread filter | `{ data: Notification[], unreadCount, pagination }` | `NotificationController.list`; newest first, recipient scoped |
| `GET /notifications/unread-count` | None | `{ data: { unreadCount } }` | `NotificationController.count` |
| `PATCH /notifications/:id/read` | None | Updated notification | `NotificationController.markRead`; 400 invalid ID, 404 wrong recipient or absent |
| `PATCH /notifications/read-all` | None | Success | `NotificationController.markAllRead`; affects caller only |

`EventService.logEvent` creates activity notifications for team or board participants, excluding the actor, after saving history. Team invitations notify the invited account. Team messages notify the other owner and accepted members. Removing a team member notifies that person after access is revoked. Notification creation failures are logged without rolling back the underlying event, invitation, or message. Existing history stays available even after a notification is marked read.
