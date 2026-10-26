# Comment API (Client)

`src/app/features/board/services/comment.ts` provides typed create and delete calls through `ApiService`. The project detail component uses `ApiService.getAllPages<Comment>` on `comments/task/:taskId`, so it can show every comment. Successful writes refresh comments and board activity. The UI exposes comment creation to board members and deletion to the comment author or Admin; it does not expose editing.
