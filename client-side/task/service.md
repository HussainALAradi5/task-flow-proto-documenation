# Task API (Client)

`src/app/features/board/services/task.ts` wraps the shared `ApiService` with typed `create`, `update`, `move`, and `delete` calls for cards. The project detail component uses `ApiService.getAllPages<Task>` to load all pages of `tasks/project/:projectId` for its local Kanban filters. A successful card write refreshes both the cards and the activity panel. Task writes return `ApiResponse<Task>`; delete returns a success message.
