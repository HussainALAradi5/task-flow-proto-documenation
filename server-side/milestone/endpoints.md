# Milestone Endpoints

## Location
`src/routes/project/milestoneRoutes.ts`

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `POST` | `/milestones` | Admin, Leader | `createMilestoneSchema` | Create milestone |
| `GET` | `/milestones` | All | - | List user's milestones |
| `GET` | `/milestones/project/:projectId` | All | - | Get milestones by project |
| `GET` | `/milestones/:id` | All | - | Get milestone by ID |
| `PATCH` | `/milestones/:id` | Admin, Leader | `updateMilestoneSchema` | Update milestone |
| `DELETE` | `/milestones/:id` | Admin, Leader | - | Soft delete milestone |

## Security Rules

- Admin and Leader can create/update/delete milestones
- `GET /milestones` - users see only milestones they created (Admin sees all)
- `GET /milestones/:id` - any authenticated user can view any milestone by ID
- `GET /milestones/project/:projectId` - any authenticated user can view milestones by project
