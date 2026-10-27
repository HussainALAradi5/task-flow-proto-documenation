# Client and server contract check

Paths below have the `/api` prefix and require login except signup and login. Checked against the current Angular components and Express routes.

| Client flow | Server route | Access and behavior |
| --- | --- | --- |
| Signup, login, profile | `POST /users/signup`, `POST /users/login`, `GET/PATCH /users/profile` | Login uses `identifier`; token is sent to the API. |
| Board list and navigation | `GET /projects`, `GET /projects/slug/:slug` | Owner, explicit board member, or Admin can read. List uses pagination. |
| Board writes | `POST /projects`, `PATCH/DELETE /projects/:id` | Any signed-in user may create. Update requires Leader or Admin and ownership for non-Admins; delete requires Admin. A new board copies its team's members. |
| Kanban cards | `GET /tasks/project/:projectId`, `POST /tasks`, `PATCH/DELETE /tasks/:id` | A board owner, member, or Admin can see and work on all cards on that board. Dragging a card sends a status PATCH; opening it offers a status control for touch and keyboard users. |
| Milestones | `GET /milestones/project/:projectId`, `POST /milestones`, `PATCH/DELETE /milestones/:id` | Board members can read. Writes need Leader or Admin and record ownership for non-Admins. |
| Comments | `GET /comments/task/:taskId`, `POST /comments`, `DELETE /comments/:id` | Board members can read and create. Comment author or Admin can delete. |
| Activity history | `GET /events/project/:projectId` | Owner, board member, or Admin sees newest-first paginated project, task, milestone, and comment activity. The client loads older pages on request. Only server services write events. |
| Teams | `GET /teams`, `POST /teams`, `PATCH/DELETE /teams/:id` | Owner, explicit member, or Admin can read. Team writes require Leader or Admin and ownership for non-Admins. |

The `demo_member` seed account belongs to Operations Group and its Operations Board, which is owned by `demo_admin`. It does not belong to Product Studio. The demo card on Operations Board is created by the Admin so shared card work can be checked. The client currently has no UI for changing team membership; the seeded relationship is stored in the team and board `members` fields.

Local server and client builds and focused tests pass. An isolated temporary MongoDB instance was used to run the seed twice and exercise the live API: all three roles logged in, Member and Leader board scopes stayed separate, the Member moved and commented on an Admin-created card, and the activity feed recorded both actions. A browser opened the real client against that API and captured the Member board, comment panel, and activity history. The other gallery images use mocked API responses shaped like the seed. The configured deployment database was not used or verified. Media upload is not exposed by the current client or server routes.
