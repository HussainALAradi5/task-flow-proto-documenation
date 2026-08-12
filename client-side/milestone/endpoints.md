# Milestone Endpoints (Client)

## API Mapping

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `getMilestones` | GET | `/milestones/project/:projectId?page=&limit=` | - |
| `getMilestone` | GET | `/milestones/:id` | - |
| `createMilestone` | POST | `/milestones` | `{ name, projectId }` |
| `updateMilestone` | PATCH | `/milestones/:id` | `{ name? }` |
| `deleteMilestone` | DELETE | `/milestones/:id` | - |
