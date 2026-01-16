# subject: [[typescript]]
## topics: #types #language-behaviors
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

## interfaces define objects, types defines any(type)thing
one of the main differences between types and interfaces. while interfaces can only declare objects, and objects can have methods, properties, etc. types can also do that (define objects) but even more.
types can define **any other type**: arrays, tuples, unions, functions, literals, mapped types and even primitives like string, number, boolean, etc.

interfaces can not extend unions. even if it's an union of objects (after all, it would result in an union ultimately):
``` typescript
type Student = {
  name: string;
  age: number;
  role: 'user';
  courses: Courses[];
}

type Teacher = {
  name: string;
  age: number;
  role: 'moderator';
  classes: Class[]
}

type User = Student | Teacher; // OK
interface Guest extends User {}; // An interface can only extend and object type or intersection of object types with statically known members.
```

also, most people say that **only interfaces and classes can be used as a class contract**. using a type would be a mistake, and throw an error:
``` typescript
type StudentRepository = {
  create: (name: string) => string;
};

class Student implements StudentsRepository { 
  create(name: string) {
    return `Welcome, ${name}!`; 
  }; 
}; // Error: A class may only implement another class or interface.
```
that's partially true. before TypeScript v2.1 that would indeed throw the error above. but since then, both `type` and `interface` keywords can define contracts and be implemented with `implements` on a class.

## hovers
hovering over types and interfaces have different implications. while hovering on an interface, only it's name shall be displayed. doing that is like creating a new type:
```typescript
interface String {
  x: string;
  y: string;
  z: string;
};

// Hovering over that would only display "String"
```

on the other hand, hovering over a type shows it's name but also it's type definition. instead of behaving like creating a new type like the interface, it behaves as if we were creating an alias.
an alias for a type could be even for an [[anonymous type]].