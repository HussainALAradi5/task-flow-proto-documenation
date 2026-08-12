# User Service (Client)

## Location
`src/app/core/auth/auth.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `signup` | `(data: SignupRequest): Observable<AuthResponse>` | Register new user |
| `login` | `(data: LoginRequest): Observable<AuthResponse>` | Authenticate user |
| `getProfile` | `(): Observable<User>` | Get current user |
| `updateProfile` | `(data: UpdateProfileRequest): Observable<User>` | Update own profile |
| `logout` | `(): void` | Clear token, navigate to login |
| `getToken` | `(): string \| null` | Get stored JWT |
| `isLoggedIn` | `(): boolean` | Check if authenticated |

## Models
```typescript
interface SignupRequest {
  userName: string;
  email: string;
  password: string;
  mobileNumber?: string;
}

interface LoginRequest {
  email: string;
  password: string;
}

interface AuthResponse {
  status: string;
  token: string;
  data: User;
}
```
