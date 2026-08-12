# User Endpoints (Client)

## API Mapping

| Service Method | HTTP | Endpoint | Body |
|----------------|------|----------|------|
| `signup` | POST | `/users/signup` | `{ userName, email, password, mobileNumber? }` |
| `login` | POST | `/users/login` | `{ email, password }` |
| `getProfile` | GET | `/users/profile` | - |
| `updateProfile` | PATCH | `/users/profile` | `{ userName?, email?, mobileNumber? }` |
