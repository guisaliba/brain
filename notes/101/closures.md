a closure is a function that remembers the environment in which it was created.
this include variables, bindings, and any piece of memory allocated even after that environment is no longer active.

this means that a closure is a function that carries both:
1. its code (what it does)
2. its environment (the captured variables it can access)

the key is that closures do not depend on the parent still being on the **stack**. when the function in which the closure was created is outlived, all of its memory is gone from the stack, but the closure still remembers the variables, bindings etc.
