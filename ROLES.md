# Roles & Permissions

## Overview

TaskFlow Proto implements a **Trello-like role-based access control (RBAC)** system with three roles. Each role has specific permissions for accessing and modifying resources.

## Roles

| Role | Value | Description |
|------|-------|-------------|
| **Admin** | `Admin` | Full system access. Can manage all users, teams, projects, and tasks. Bypasses all data isolation filters. |
| **Leader** | `Leader` | Team leader. Can create projects, manage team tasks, and view team members. Auto-promoted when creating a project. |
| **Member** | `Member` | Default role. Can view and edit assigned tasks only. Limited to own records. |

## Role Assignment

- **Default:** New users receive `Member` role on signup
- **Auto-Promotion:** Creating a project automatically promotes `Member` to `Leader`
- **Manual:** Only `Admin` can change user roles via `PATCH /api/users/:id/role`

## Permissions Matrix

### User Management

| Action | Admin | Leader | Member |
|--------|:-----:|:------:|:------:|
| Create user (signup) | - | - | - (public) |
| View all users | ✅ | ❌ | ❌ |
| View team members | ✅ | ✅ | ❌ |
| View own profile | ✅ | ✅ | ✅ |
| Update own profile | ✅ | ✅ | ✅ |
| Change user role | ✅ | ❌ | ❌ |
| Delete/deactivate user | ✅ | ❌ | ❌ |

### Team Management

| Action | Admin | Leader | Member |
|--------|:-----:|:------:|:------:|
| Create team | ✅ | ✅ | ❌ |
| View all teams | ✅ | ❌ | ❌ |
| View own team | ✅ | ✅ | ✅ |
| Update team | ✅ | ✅ (own) | ❌ |
| Delete team | ✅ | ❌ | ❌ |

### Project Management

| Action | Admin | Leader | Member |
|--------|:-----:|:------:|:------:|
| Create project | ✅ | ✅ | ❌ |
| View all projects | ✅ | ❌ | ❌ |
| View team projects | ✅ | ✅ | ❌ |
| View assigned projects | ✅ | ✅ | ✅ |
| Update project | ✅ | ✅ (team) | ❌ |
| Delete project | ✅ | ❌ | ❌ |

### Task Management

| Action | Admin | Leader | Member |
|--------|:-----:|:------:|:------:|
| Create task | ✅ | ✅ (team) | ❌ |
| View all tasks | ✅ | ❌ | ❌ |
| View project tasks | ✅ | ✅ (team) | ❌ |
| View assigned tasks | ✅ | ✅ | ✅ |
| Update any task | ✅ | ✅ (team) | ❌ |
| Update assigned task | ✅ | ✅ | ✅ |
| Delete task | ✅ | ✅ (team) | ❌ |

### Milestone Management

| Action | Admin | Leader | Member |
|--------|:-----:|:------:|:------:|
| Create milestone | ✅ | ✅ (team) | ❌ |
| View all milestones | ✅ | ❌ | ❌ |
| View project milestones | ✅ | ✅ (team) | ✅ (project) |
| Update milestone | ✅ | ✅ (team) | ❌ |
| Delete milestone | ✅ | ✅ (team) | ❌ |

### Event/Audit Log

| Action | Admin | Leader | Member |
|--------|:-----:|:------:|:------:|
| View all events | ✅ | ❌ | ❌ |
| View own events | ✅ | ✅ | ✅ |
| Create event | ✅ | ✅ | ✅ |

## Data Isolation Rules

### Admin
- Sees **all** records across the system
- Bypasses `createdBy` filter
- Can modify any record

### Leader
- Sees records they created
- Sees records within their team (when `teamId` is set)
- Can create projects (auto-promotes from Member)
- Can manage tasks within team projects

### Member
- Sees only records they created (`createdBy` filter)
- Can view and update tasks assigned to them (`assignTo` field)
- Cannot create projects or milestones
- Cannot manage teams

## Implementation

### Middleware Stack

```
router.use(protect);           // Verify JWT, attach user
router.use(restrictTo('Admin')); // Admin-only routes
```

### Controller-Level Filtering

```typescript
// BaseController - user data isolation
getAll = catchAsync(async (req, res) => {
  let filter = { ...req.query };
  
  if (req.user?.role !== UserRole.ADMIN) {
    filter.createdBy = req.user.id;
  }
  
  const items = await this.service.getAll(filter);
  res.json({ status: 'success', data: items });
});
```

### Service-Level Filtering

```typescript
// TaskService - get tasks by project with user isolation
async getMyTasksByProject(projectId: string, userId: string): Promise<ITask[]> {
  const filter = { 
    projectId: new Types.ObjectId(projectId),
    createdBy: new Types.ObjectId(userId)
  };
  return await this.getAll(filter);
}
```

## Future Enhancements

- [ ] Team-based project scoping (filter by `teamId` instead of `createdBy`)
- [ ] Granular permissions (e.g., `task:assign`, `project:delete`)
- [ ] Custom roles with permission sets
- [ ] Role hierarchy (Leader inherits Member permissions)
- [ ] Audit trail for permission changes
