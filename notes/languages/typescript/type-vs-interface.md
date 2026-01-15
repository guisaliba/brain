# subject: [[typescript]]
## topics: #typescript #web-development 
## source: [type-vs-interface](https://www.alvseven.com/type-vs-interface)
---
## background
in the beggining, typescript didn't even have the `type` that we know these days. the keyword itself was introduced only on TypeScript v1.4, which is 6 releases after the first release.
in the other hand, interfaces were always there. you'd use them to define objects, and that was it. wanted to define a string literal, conditional types, etc? you couldn't.
the `type` feature made that and many other things possible.

the first conception was that `types` would only be used to define things like tuples, unions, functions, arrays, etc. but **NOT** objects. that was on the `interface` domain only.
using types for object literals would throw an error:
```typescript
type Lesson = {
  subject: string;
  topics: Array<string>;
  source: string | URI;
} 

// Error: Aliased type cannot be an object type literal.
// Use an interface declaration instead.

```

so the rule was pretty simple: *use interfaces to define objects. otherwise, use types.*
that eventually came up to change. here's the [pull request](https://github.com/microsoft/TypeScript/pull/957) that introduced the `type` keyword, and here is the [pull request](https://github.com/microsoft/TypeScript/pull/1025) that removed the object definition restriction.


