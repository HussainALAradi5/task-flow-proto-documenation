# User Service (Client)

## Location
`src/app/core/services/auth.service.ts`

## Methods

| Method | Signature | Description |
|--------|-----------|-------------|
| `signup` | `(data: SignupRequest): Observable<AuthResponse>` | Register new user |
| `login` | `(data: LoginRequest): Observable<AuthResponse>` | Authenticate user |
| `getProfile` | `(): Observable<{ status: string; data: User }>` | Get current user |
| `updateProfile` | `(data: Partial<User>): Observable<{ status: string; data: User }>` | Update own profile |
| `logout` | `(): void` | Clear token, navigate to login |
| `getToken` | `(): string \| null` | Get stored JWT |
| `isLoggedIn` | `Signal<boolean>` | Check whether a profile is loaded |

## Models
```typescript
interface SignupRequest {
  userName: string;
  email: string;
  password: string;
  mobileNumber?: string;
}

interface LoginRequest {
  identifier: string;
  password: string;
}

interface AuthResponse {
  status: string;
  token: string;
  data: User;
}
```
