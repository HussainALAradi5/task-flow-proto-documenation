# Free live demo: Render and MongoDB Atlas

This setup publishes the Angular client as a Render Static Site, runs the Express API as a Render Free Web Service, and stores data in a MongoDB Atlas Free cluster. It is suitable for a demo or small pilot. The API sleeps after inactivity, so the first request can take about a minute. Free hosting does not provide the availability and operational safeguards needed for a public production launch.

The client, server, and documentation are separate Git repositories. In Render, connect the **client** and **server** repositories separately. The `render.yaml` in their parent folder is not in either Git repository and will not be discovered by Render.

## 1. Create the database

1. Create a MongoDB Atlas **Free** cluster and a database user with a unique, strong password.
2. Copy its `mongodb+srv://...` connection string. Replace the placeholders and include a database name such as `taskflow_demo`. Keep the URI private.
3. After creating the Render API service, open its **Connect > Outbound** tab. Add its outbound IP ranges to the Atlas **Network Access** list. Atlas must allow the API's addresses before the API can start.

Use a dedicated demo database. Do not point this deployment at an existing personal or production database.

## 2. Deploy the API

In Render, choose **New > Web Service**, connect [`task-flow-proto-server-side`](https://github.com/HussainALAradi5/task-flow-proto-server-side), and use:

| Setting | Value |
| --- | --- |
| Runtime | Node |
| Instance type | Free |
| Root directory | Repository root (leave blank) |
| Build command | `npm ci --include=dev && npm run build` |
| Start command | `npm start` |
| Health check path | `/` |

Set these environment variables in Render, not in Git:

| Key | Value |
| --- | --- |
| `NODE_ENV` | `production` |
| `NODE_VERSION` | `24` |
| `MONGO_URI` | Atlas connection string from step 1 |
| `JWT_SECRET` | A unique, long random secret |
| `CORS_ORIGINS` | The exact client URL from step 3, with no trailing slash |

Render provides `PORT`; the server reads it. Save the assigned API URL. Open its root URL and expect `TaskFlowProto API is running`. If startup fails, check the Render logs, Atlas URI, database user, and Atlas IP access list.

The current API is [taskflow-proto-api.onrender.com](https://taskflow-proto-api.onrender.com/). With `NODE_ENV=production`, npm otherwise omits the TypeScript development dependencies during the Render build, so keep `--include=dev` in the build command.

## 3. Deploy the client

The production client currently points to `https://taskflow-api.onrender.com/api` in `src/environments/environment.prod.ts`. If the API URL assigned in step 2 differs, change that file in the **client repository**, commit, and push before deploying the client. Append `/api` to the API origin. Do not put database credentials or `JWT_SECRET` in the Angular client.

In Render, choose **New > Static Site**, connect [`task-flow-proto-client-side`](https://github.com/HussainALAradi5/task-flow-proto-client-side), and use:

| Setting | Value |
| --- | --- |
| Root directory | Repository root (leave blank) |
| Build command | `npm ci && npm run build` |
| Publish directory | `dist/task-flow-proto-client-side/browser` |

Add a static-site **Rewrite** rule: source `/*`, destination `/index.html`. This lets Angular routes load after a browser refresh.

Copy the static site's exact `https://...onrender.com` URL into the API's `CORS_ORIGINS` environment variable and redeploy the API. Do not append `/api` or a path to the CORS origin.

The current client is [taskflow-proto-client.onrender.com](https://taskflow-proto-client.onrender.com). Its API URL is `https://taskflow-proto-api.onrender.com/api`, and the API allows the client origin in `CORS_ORIGINS`.

## 4. Verify the live demo

1. Open the static-site URL, create a user, sign in, and refresh a board route directly.
2. Create a board and card; drag the card to another column; add a comment; confirm the activity history records those actions.
3. If you want the three sample roles, run the [demo seed](README.md#demo-seed) from a trusted local machine with `MONGO_URI` set to this **dedicated demo database** and a new `DEMO_SEED_PASSWORD`. Do not expose sample account credentials on a public deployment.

For public production use, verify backup and recovery, monitoring, authentication protection, and deployed end-to-end behavior before inviting real users.
