# subject: [[typescript]]
## topics: #types #language-behaviors
---
an anonymous type in TypeScript is any (not the "any" type) type written inline, without having been given a named alias (like an `interface` or a `type`):
```typescript
function getUser(user: { name: string }): string {
  const user: string = await db.query(name);
  return `User found: ${user}`
};
```

`{ name: string }` is an anonymous type. it has no name, but it's still a type.
these can be used anywhere you'd otherwise use `interface/type`, e.g.:
```typescript
type User = { name: string };
function getUser(user: User): User { ... }

// This could also be written as:
function getUser(user: { name: string }): { name: string } { ... }
```

anonymous types are good for:
- local shapes
- simple signatures
- no need for reuse
while named types are quite the opposite:
- improve reuse
- give good readability
- enhance error messages when used in multiple places