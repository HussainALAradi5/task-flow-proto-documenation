# Team API (Client)

`src/app/features/team/services/team.ts` wraps `ApiService` for paginated team listing, create, update, delete, invitations, and member removal. Team owners or Admins invite an existing account by email. The recipient sees a pending count in the header and can accept or decline on the Teams page. Membership and access to that team's active boards are added only after acceptance. Member users can read teams they explicitly belong to.
