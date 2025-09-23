a closure is a function that remembers the environment in which it was created.
this include variables, bindings, and any piece of memory allocated even after that environment is no longer active.

this means that a closure is a function that carries both:
1. its code (what it does)
2. its environment (the captured variables it can access)

the key is that closures do not depend on the parent still being on the **stack**.