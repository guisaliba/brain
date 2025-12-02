**React Server Components (RSC)** are a new paradigm in React where components render **exclusively on the server**.

Unlike traditional React components (which render on the server _and_ then "hydrate" or run again in the browser), Server Components:

1. **Never run in the browser.** Their code is not included in the JavaScript bundle sent to the client.
2. **Can be Async.** They can use `async/await` directly in the component body to fetch data.
3. **Have direct backend access.** They can connect directly to databases or read file systems.