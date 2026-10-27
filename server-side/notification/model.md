# Notification model and service

`src/models/Notification.ts` stores `recipient` (User ObjectId), `kind` (`NotificationKind` enum: `activity`, `invitation`, `message`), `title`, `description`, local `href`, nullable `readAt`, and `createdAt`. The schema indexes recipient with creation time and read state. The TypeScript shape is in `src/interface/Notification.ts`.

`src/services/NotificationService.ts` exposes `invitation(userId, teamName)`, `teamMessage(teamId, teamName, owner, members, actorId)`, and `activity(title, entityType, entityId, description, actorId?)`. It resolves the current team or project membership when creating notifications; it never accepts client-supplied recipient IDs or links.
