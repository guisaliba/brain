a closure is a function that remembers the environment in which it was created.
this include variables, bindings, and any piece of memory allocated even after that environment is no longer active.

this means that a closure is a function that carries both:
1. its code (what it does)
2. its environment (the captured variables it can access)

the key is that closures do not depend on the parent still being on the **stack**. when the function in which the closure was created is outlived, all of its memory is gone from the stack, but the closure still remembers the variables, bindings etc.

the runtime keeps the captured variables alive for as long as the closure referencing them is alive.

```js
function makeCounter() {
  let count = 0; // local variable

  return function() { // this is the closure
    count++;
    return count;
  };
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

this can be visualized through a mental model:
- usually, local variables live on the stack and disappear when the function returns
- when a closure **captures** a variable, the runtime "lifts" that variable from the stack into the **heap**, so it outlives the function call
- both the closure and any other closures share references to the same memory

they are not tied to when the parent executes, they're tied to variable lifetimes and variables live as long as there are closures referencing them.

so in the `makeCounter` example:
- The variable `count` isn’t duplicated for each call of `counter()` — it’s one shared piece of state living on the heap.
    
- That’s why successive calls keep incrementing instead of starting fresh.

in higher-level languages, the garbage collector takes care of this cleanup.
