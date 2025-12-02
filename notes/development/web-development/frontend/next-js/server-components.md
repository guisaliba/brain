**React Server Components (RSC)** are a new paradigm in React where components render **exclusively on the server**.

Unlike traditional React components (which render on the server _and_ then "hydrate" or run again in the browser), Server Components:
1. **Never run in the browser.** Their code is not included in the JavaScript bundle sent to the client.
2. **Can be Async.** They can use `async/await` directly in the component body to fetch data.
3. **Have direct backend access.** They can connect directly to databases or read file systems.

 In the Next.js App Router, every component is a **Server Component by default**. To make it a Client Component, you must add the directive `"use client"` at the very top of the file.

does that mean server data is exclusively to Server Components? can Client ones access it?

**Directly? No.**  
Client Components run in the user's browser (after being pre-rendered on the server). They cannot reach into your database or read the incoming HTTP request headers directly because they are running on the user's laptop, not your server.

**Indirectly? Yes.**  
They access server data by:
1. **Props:** A Server Component fetches data and passes it down to the Client Component as props.
2. **API Routes / Server Actions:** The Client Component makes an AJAX request (fetch) to your server to ask for data.
