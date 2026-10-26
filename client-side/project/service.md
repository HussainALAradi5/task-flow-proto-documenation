# Project API (Client)

`src/app/features/board/services/project.ts` wraps the shared `ApiService` for paginated project listing, create, update, delete, and slug lookup. The board component uses this typed service; after creating a project it refreshes the profile because a Member creator becomes a Leader. The detail page loads a board by slug through the same service. Writes return `ApiResponse<Project>`; delete returns a success message.
