# Team model in the client

Location: `src/app/core/interfaces/team.interface.ts`.

`Team` extends `BaseEntity` with `name`, optional `description`, and optional `members`. A member is an ID or a populated user object with `_id`, `userName`, and `email`. Team list responses are paginated and may populate members. Create and edit forms send name and description. Member management sends invitations, and the recipient must accept before appearing in the members list. The demo seed provides the initial Operations Group membership.
