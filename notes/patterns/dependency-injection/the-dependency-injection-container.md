key concepts of dependency injection is inversion of control (IoC) where instead of an object creating its own dependencies, they are provided to it from an external source.
the DI container is the one responsible for instantiating and managing dependencies instead of the object itself.

## registration (binding) phase
the container "knows" which implementations to provide for specific interfaces or classes. stating that the container knows it actually means it should know, which in other words means it must be configured to know and resolve that.
 
example:

```pseudo
container.register(ServiceInterface, ConcreteService)
container.register(DatabaseConnection, new PgDatabaseConn(db-info))
```

here the DI container registers a key-value pair. the key is the abstract type (e.g.: an interface) and the value is the concrete implementation of that type (it could also be a factory function for custom instantiation logic or an already created instance e.g.: a singleton).

example:

```pseudo
container.register("ServiceInterface", FastService)
// { "key": "ServiceInterface", "value": FastService }
```

the `value` can be a concrete type (e.g.: `FastService`), a function (e.g.: `() => new FastService()`) or a pre-existing instance such as a singleton.
## resolution phase
when an object is requested, the DI container locates the appropriate dependency first, matching the requested type (either it be a class or interface) with its registered concrete implementation.

if a dependency requires its own dependencies, the container resolves it recursively and provides those too. then it returns the fully constructed object.

example:

```pseudo
// assuming ServiceInterface has a registered implementation for it
service = container.resolve(ServiceInterface)
```
## injection mechanisms
the container uses specific injection methods to provide dependencies
### constructor injection
dependencies are passed as constructor arguments:

```pseudo
class MyService {
  prop db
  
  constructor(databaseConn) { this.db = databaseConn }
}
```
### property injection
dependencies are passed using properties:

```pseudo
class MyService {
  prop db
  
  setDatabaseConnection(db){
    this.db = db
  }
}
```
## lifecycle management
the container manages the lifecycle of dependencies to control their scope:

- **singleton**: a single instance of the dependency is created across the application.
- **transient**: a new instance of the dependency is created each time it's requested.
- **scoped**: instances are created for specific contexts (e.g.: per web request).
