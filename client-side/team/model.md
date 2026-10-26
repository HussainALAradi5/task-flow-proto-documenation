# Team model in the client

Location: `src/app/core/interfaces/team.interface.ts`.

`Team` extends `BaseEntity` with `name`, optional `description`, and optional `members`. A member is an ID or a populated user object with `_id`, `userName`, and `email`. Team list responses are paginated and may populate members. Create and edit forms currently send only name and description; the demo seed provides the Operations Group membership.
