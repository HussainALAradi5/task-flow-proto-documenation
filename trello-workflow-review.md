# Trello-style workflow review

This review compares TaskFlow's implemented collaboration flow with the requested board experience. It documents design choices and remaining limits.

| Workflow | Current implementation |
| --- | --- |
| Boards and cards | Projects are boards with To Do, In Progress, In Review, and Done columns. Cards can be moved by drag and drop or with the status control. |
| Teams as workspaces | A Team groups boards. The owner can invite an existing account by email. The recipient sees a header badge and can accept or decline from Teams. Acceptance grants access to the team and its active boards. Removal revokes that inherited access. Team leader/member badges describe the person's role in that team; the profile badge describes their account role. |
| Team boards and views | Teams show linked boards. Boards show distinct Personal board and Team board badges plus the team name. Projects can be filtered to All, My projects, or Team projects; board and team collections can be viewed as a grid or list. |
| Team chat | The owner and accepted team members can post text and one small verified image, GIF, PDF, or text file. The composer supports drag and drop, an emoji picker, and `@` suggestions from accepted members. The server checks mentioned IDs against team membership and gives mentioned people a distinct notice. The drawer loads recent messages and older pages; it refreshes every 15 seconds while open. |
| Inbox | A protected notification page lists invitation, team message, and activity notices with unread state, filters, pagination, and read actions. The header bell shows unread count. |
| Sign in | Email is the primary identifier in the form and is matched without case sensitivity or surrounding spaces. Username and mobile remain supported. |
| Card discussion | Board members can post chronological text comments or one small PNG, JPEG, GIF, or WebP image per comment. The API verifies file signatures and limits images to 500 KB. Comments and image data persist in MongoDB. |
| History | The board activity panel records server-side project, card, milestone, comment, and team actions; the client loads older pages. |
| Dates | Task creation, start, target, end, and delivery dates must be chronological. Forms provide date minimums and show errors; the API enforces the same rule on create and update. |
| Access | Boards are private to the owner, explicit members, and Admin. A team invite requires consent before access is granted. Only the team creator manages team details and members. |

## Deliberate limits

- Invitations are delivered inside TaskFlow to registered accounts. Email delivery needs a transactional email provider and verified sender domain, which are not configured on the free deployment.
- Teams serve the organization/workspace role. Separate organization billing and administration are not implemented.
- Public boards are not enabled. They would expose tasks, discussion, and attachments through anonymous routes, so this needs a separate privacy design and explicit visibility controls.
- Files larger than 500 KB, multiple files per message, and external GIF search need a separate storage/media design. This prototype stores one small verified file directly in the protected MongoDB message document; Render's temporary filesystem is not used.
- This is a Trello-inspired prototype, not feature parity with Trello (for example, no checklists, automation, or board templates).

## Regression checks

Run server and client builds and tests. In an isolated MongoDB instance, verify: team member and unrelated Admin cannot edit or invite; owner can invite; accepted member can chat while outsider and unrelated Admin cannot; project scope filters retain access rules; another user cannot mark a notification read; unread count falls after read-all. Earlier checks also covered invitation consent, date rejection, valid GIF comments, and access revocation. In the browser, test the bell, read/unread filter, team chat, board badges and filters, grid/list controls, and invitation actions with Leader and Member accounts.

On October 28, 2026, the client and server builds passed, the client tests passed (2/2), and the server tests passed (10/10). After deployment, the live API rejected a PDF with a mismatched `.html` filename, then accepted a small PDF and a mention of a current Operations Group member. The message was read back with its filename and mention ID. The public client served the new bundle. The attachment and mention interaction in the rendered chat UI still needs a manual browser pass.
