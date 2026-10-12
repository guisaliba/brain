# subject: [[nestjs]]
# topics: #nestjs #auth 
---
## 🔑 What is Passport?
- **Passport** is a **Node.js authentication library**.
- It provides a **plug-and-play way** to authenticate requests using _strategies_.
- Instead of writing login logic for every method (JWT, OAuth, username/password…), you just configure a **strategy** and Passport does the heavy lifting.
Think of Passport like a **Swiss Army knife for auth** — each "blade" is a **strategy**.
---
## 🧭 What is an Authentication Strategy?
A **strategy** is simply an algorithm (with some config) that defines **how a request should be authenticated**.

Examples in general Node/Express:
- `passport-local` → authenticate with username + password.
- `passport-jwt` → authenticate with a JWT extracted from headers.
- `passport-oauth2` → authenticate via OAuth2 flow (Google, GitHub, etc.).
Each strategy
1. Extracts credentials from the request (e.g., header, cookie, form).
2. Validates those credentials (e.g., verify password hash, check JWT signature).
3. If valid → attaches a `user` object to `req.user`.  
    If invalid → signals authentication failure.
---
## 🛡️ Passport in NestJS
NestJS wraps Passport neatly with:
- `@nestjs/passport` package.
- `PassportStrategy` class to create your own strategies.
- `AuthGuard('strategyName')` to connect guards with strategies.
So **AuthGuard** is essentially a NestJS wrapper around Passport’s strategy execution.
---
## ⚙️ Example: Local Strategy (username/password)
### Step 1. Define the strategy

``` typescript
// local.strategy.ts
@Injectable()
export class LocalStrategy extends PassportStrategy(Strategy) {
  constructor(private authService: AuthService) {
    super(); // tells passport-local to expect "username" and "password" fields by default
  }

  async validate(username: string, password: string): Promise<any> {
    const user = await this.authService.validateUser(username, password);
    if (!user) {
      throw new UnauthorizedException();
    }
    return user; // this becomes req.user
  }
}
```

Step 2. Create the guard

``` typescript
// auth.guard.ts
@Injectable()
export class LocalAuthGuard extends AuthGuard('local') {}
```

Step 3. Use it in a controller

``` typescript
// auth.controller.ts
@Controller('auth')
export class AuthController {
  @UseGuards(LocalAuthGuard)
  @Post('login')
  async login(@Request() req) {
    return this.authService.login(req.user); // req.user comes from strategy
  }
}
```

---

## ⚙️ Example: JWT Strategy
### Step 1. Define the strategy

``` typescript
// jwt.strategy.ts
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      secretOrKey: 'secretKey',
    });
  }

  async validate(payload: any) {
    return { userId: payload.sub, username: payload.username };
  }
}
```
### Step 2. Create the guard

``` typescript
@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {}
```

### Step 3. Protect routes

``` typescript
@Controller('users')
export class UsersController {
  @UseGuards(JwtAuthGuard)
  @Get('profile')
  getProfile(@Request() req) {
    return req.user;
  }
}
```

## 🔗 How it all connects
- **Strategy** = defines _how_ to authenticate (JWT, Local, OAuth, etc.).
- **AuthGuard('strategyName')** = tells NestJS to use that strategy for this route.
- **req.user** = if authentication succeeds, Passport puts the validated user here.
- **Your code** = can now rely on `req.user` without rechecking credentials.
---
## 🧠 TL;DR
- **Passport** = library for authentication.
- **Strategy** = method of authentication (local, JWT, OAuth, etc.).
- **AuthGuard** = NestJS way of plugging strategies into guards.

Guards in general decide **if access is granted**.  
AuthGuards specifically delegate that decision to a Passport strategy.