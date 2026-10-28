# User Endpoints

## Location
`src/routes/user/authRoutes.ts`, `src/routes/user/userRoutes.ts`

## Public (No Auth)

| Method | Endpoint | Validation | Description |
|--------|----------|------------|-------------|
| `POST` | `/users/signup` | `signupSchema` | Register new user |
| `POST` | `/users/login` | `loginSchema` | Authenticate with email, username, or mobile and password; email ignores case and surrounding spaces |

## Protected (Auth Required)

| Method | Endpoint | Roles | Validation | Description |
|--------|----------|-------|------------|-------------|
| `GET` | `/users/profile` | All | - | Get own profile |
| `PATCH` | `/users/profile` | All | `updateUserSchema` | Update own profile |
| `GET` | `/users` | Admin | - | List all users |
| `GET` | `/users/:id` | Admin | - | Get user by ID |
| `PATCH` | `/users/:id` | Admin | `updateUserSchema` | Update any user |
| `DELETE` | `/users/:id` | Admin | - | Soft delete user |
| `PATCH` | `/users/:id/role` | Admin | `updateRoleSchema` | Change user role |

## Security Rules

- User can only view/edit their own profile
- `GET /users` - Admin only, lists all users
- `GET /users/:id` - Admin only
- `PATCH /users/:id` - Admin only
- `DELETE /users/:id` - Admin only
- Only Admin can change roles
- Passwords never returned in responses
- Email addresses are stored lowercase on signup/profile update. Existing mixed-case email records still match at login. Duplicate-email checks ignore case.
