# User Endpoints

## Public (No Auth)

| Method | Endpoint | Body | Response |
|--------|----------|------|----------|
| `POST` | `/users/signup` | `{ userName, email, password, mobileNumber? }` | `{ token, data: User }` |
| `POST` | `/users/login` | `{ email, password }` | `{ token, data: User }` |

## Protected (Auth Required)

| Method | Endpoint | Roles | Body | Description |
|--------|----------|-------|------|-------------|
| `GET` | `/users/profile` | All | - | Get own profile |
| `PATCH` | `/users/profile` | All | `{ userName?, email?, mobileNumber? }` | Update own profile |
| `GET` | `/users` | Admin | - | List all users |
| `GET` | `/users/:id` | Admin | - | Get user by ID |
| `PATCH` | `/users/:id` | Admin | `{ userName?, email?, mobileNumber? }` | Update any user |
| `DELETE` | `/users/:id` | Admin | - | Soft delete user |
| `PATCH` | `/users/:id/role` | Admin | `{ role }` | Change user role |

## Security Rules
- User can only edit their own profile
- Only Admin can view/edit/delete other users
- Only Admin can change roles
