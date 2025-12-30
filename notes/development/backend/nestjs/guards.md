# subject: [[nestjs]]
# topics: #nestjs #auth
---
## 🛡️ What is a Guard in NestJS?
Think of a **Guard** like a **bouncer at a nightclub**:
- Its only job is to **decide if the request is allowed to proceed**.
- It sits right before the controller’s route handler executes.
- If the guard says "yes" (`true`), Nest lets the request enter the controller.
- If it says "no" (`false` or throws an exception), the request is rejected.

Formally:
- Guards implement the `CanActivate` interface.
- They receive an `ExecutionContext` (which wraps around the request/response + extra NestJS metadata).
- They return a boolean or a Promise/Observable of boolean.

Example (classic **AuthGuard**):
``` typescript
@Injectable()
export class AuthGuard implements CanActivate {
  canActivate(context: ExecutionContext): boolean {
    const request = context.switchToHttp().getRequest();
    return request.headers.authorization === "valid-token";
  }
}
```

➡️ If `true`, controller runs. If `false`, request is denied.

---
## ⚙️ How are Guards Different from Middlewares?
Both look similar at first glance (they run before the controller), but:

| Aspect             | **Middleware**                                                        | **Guard**                                                                                   |
| ------------------ | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Level**          | Runs before guards/pipes/filters, closer to raw Express/Fastify layer | Runs **inside Nest’s lifecycle**, after middleware but before interceptors & route handlers |
| **Purpose**        | Request preprocessing (logging, body parsing, adding props to `req`)  | **Authorization / access control** (decide if route can be executed)                        |
| **Return**         | Usually `next()` to keep flow moving                                  | Must return `true`/`false` (or throw) to allow/block                                        |
| **Context Access** | Has direct access to `req`, `res`, `next`                             | Gets a richer `ExecutionContext` (can work in HTTP, WebSockets, RPC, etc.)                  |
| **Scope**          | Applied at app/global/route level                                     | Applied at global/module/controller/method level                                            |
## 📊 TL;DR
- **Middleware** = "pre-processing" (change request, log, validate raw headers, etc.).
- **Guard** = "authorization gatekeeper" (decide if route can run).
- Middleware is about **shaping the request**, Guards are about **allowing or denying execution**.