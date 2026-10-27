# Client and server contract check

Paths below have the `/api` prefix and require login except signup and login. Checked against the current Angular components and Express routes.

| Client flow | Server route | Access and behavior |
| --- | --- | --- |
| Signup, login, profile | `POST /users/signup`, `POST /users/login`, `GET/PATCH /users/profile` | Login uses `identifier`; token is sent to the API. |
| Board list and navigation | `GET /projects`, `GET /projects/slug/:slug` | Owner, explicit board member, or Admin can read. List uses pagination. |
| Board writes | `POST /projects`, `PATCH/DELETE /projects/:id` | Any signed-in user may create. Update requires Leader or Admin and ownership for non-Admins; delete requires Admin. A new board copies its team's members. |
| Kanban cards | `GET /tasks/project/:projectId`, `POST /tasks`, `PATCH/DELETE /tasks/:id` | A board owner, member, or Admin can see and work on all cards on that board. Dragging a card sends a status PATCH; opening it offers a status control for touch and keyboard users. |
| Milestones | `GET /milestones/project/:projectId`, `POST /milestones`, `PATCH/DELETE /milestones/:id` | Board members can read. Writes need Leader or Admin and record ownership for non-Admins. |
| Comments | `GET /comments/task/:taskId`, `POST /comments`, `DELETE /comments/:id` | Board members can read and create. Comment author or Admin can delete. Comments display oldest first and may include a validated PNG, JPEG, GIF, or WebP attachment up to 500 KB. |
| Activity history | `GET /events/project/:projectId` | Owner, board member, or Admin sees newest-first paginated project, task, milestone, and comment activity. The client loads older pages on request. Only server services write events. |
| Teams and invitations | `GET /teams`, `POST /teams`, `PATCH/DELETE /teams/:id`, `POST /teams/:id/members`, `GET /teams/invitations/pending`, `POST /teams/invitations/:id/respond` | Owner, explicit member, or Admin can read. An owner/Admin sends an in-app invitation to an existing account; the recipient must accept before team and board access is added. |

The `demo_member` seed account belongs to Operations Group and its Operations Board, which is owned by `demo_admin`. It does not belong to Product Studio. The demo card on Operations Board is created by the Admin so shared card work can be checked. New members are invited from Teams; they see invitations in their Teams page and choose Accept or Decline.

Local server and client builds and focused tests pass. An isolated temporary MongoDB instance was used to run the seed twice and exercise the API: all three roles logged in, Member and Leader board scopes stayed separate, the Member moved and commented on an Admin-created card, and the activity feed recorded both actions. The 2026-10-27 integration check also verified invitation rejection for outsiders, duplicate prevention, recipient acceptance, access before and after acceptance, invalid task date rejection, a GIF comment, and revocation on member removal. The deployment database was seeded separately. In the deployed browser, the Leader invited the Member, the Member saw the header badge and accepted, gained access to the Leader's boards, and then the Leader removed that temporary access. The task form showed a date error for a target before creation. The gallery includes deployed invitation and discussion screenshots alongside the isolated role screenshots.
