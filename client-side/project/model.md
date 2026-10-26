# Project model in the client

Location: `src/app/core/interfaces/project.interface.ts`.

`Project` extends `BaseEntity` with `title`, optional `description`, optional `teamId`, and optional `members`. A member is an ID or populated user object. The board list is paginated. Project creation sends title, description, and optional team ID; the server copies the team's members into the board on creation.
