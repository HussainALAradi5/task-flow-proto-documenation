# Notifications in the client

`src/app/core/services/notification.service.ts` wraps list, unread count, single read, and read-all calls. The client `Notification` interface and `NotificationKind` enum are separate from the service. The header shows the unread count and refreshes it every 30 seconds while signed in. The protected `/notifications` page has All and Unread filters, read/unread styling, pagination, Mark as read, Mark all as read, and an Open action. Invitation links open Teams; team message links open the relevant team chat; board activity links open its board.
