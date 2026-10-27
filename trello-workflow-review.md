# Trello-style workflow review

This review compares TaskFlow's implemented collaboration flow with the requested board experience. It documents design choices and remaining limits.

| Workflow | Current implementation |
| --- | --- |
| Boards and cards | Projects are boards with To Do, In Progress, In Review, and Done columns. Cards can be moved by drag and drop or with the status control. |
| Teams as workspaces | A Team groups boards. The owner can invite an existing account by email. The recipient sees a header badge and can accept or decline from Teams. Acceptance grants access to the team and its active boards. Removal revokes that inherited access. |
| Card discussion | Board members can post chronological text comments or one small PNG, JPEG, GIF, or WebP image per comment. The API verifies file signatures and limits images to 500 KB. Comments and image data persist in MongoDB. |
| History | The board activity panel records server-side project, card, milestone, comment, and team actions; the client loads older pages. |
| Dates | Task creation, start, target, end, and delivery dates must be chronological. Forms provide date minimums and show errors; the API enforces the same rule on create and update. |
| Access | Boards are private to the owner, explicit members, and Admin. A team invite requires consent before access is granted. |

## Deliberate limits

- Invitations are delivered inside TaskFlow to registered accounts. Email delivery needs a transactional email provider and verified sender domain, which are not configured on the free deployment.
- Teams serve the organization/workspace role. Separate organization billing and administration are not implemented.
- Public boards are not enabled. They would expose tasks, discussion, and attachments through anonymous routes, so this needs a separate privacy design and explicit visibility controls.
- Images larger than 500 KB, file attachments, and external GIF search need object storage or a media provider. Render's free web server filesystem is temporary, so uploads are stored in the database within a small size limit.
- This is a Trello-inspired prototype, not feature parity with Trello (for example, no checklists, automation, or board templates).

## Regression checks

Run server and client builds and tests. In an isolated MongoDB instance, verify: outsider cannot invite; owner can invite once; recipient cannot see team/board before accepting; other users cannot respond; acceptance grants board access; invalid task dates return 400; a valid GIF comment persists; removal revokes inherited board access. In the browser, test the invitation badge, accept/decline buttons, card discussion, and date error messages with Leader and Member accounts.
