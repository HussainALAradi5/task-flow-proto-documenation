# Event API in the client

The project detail page calls `ApiService.getAll<ActivityEvent>` with the path `events/project/${projectId}` and `{ page, limit: 10 }`. It loads page 1 when the board opens and after card, milestone, or comment changes, and appends the next page when the user selects **Load older activity**. It renders the event title, description, acting user, and timestamp. A load failure shows an error and a Refresh action. The server creates and orders history; the client has no event write call.
