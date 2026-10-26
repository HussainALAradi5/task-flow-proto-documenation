# Milestone API (Client)

`src/app/features/board/services/milestone.ts` provides typed create, update, and delete calls through `ApiService`. The project detail component uses `ApiService.getAllPages<Milestone>` on `milestones/project/:projectId` so all milestones are shown. Successful writes refresh the milestone list and activity history. The UI shows milestone write controls only to the board owner with the Leader role or an Admin.
