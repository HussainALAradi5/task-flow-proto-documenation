# Team API (Client)

`src/app/features/team/services/team.ts` wraps `ApiService` for paginated team listing, create, update, and delete. The team component uses this typed service and shows create/edit controls to Leaders or Admins, while the server enforces ownership on writes. Member users can read teams they explicitly belong to.
