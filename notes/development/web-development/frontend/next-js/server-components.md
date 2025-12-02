**React Server Components (RSC)** are a new paradigm in React where components render **exclusively on the server**.

Unlike traditional React components (which render on the server _and_ then "hydrate" or run again in the browser), Server Components:
1. **Never run in the browser.** Their code is not included in the JavaScript bundle sent to the client.
2. **Can be Async.** They can use `async/await` directly in the component body to fetch data.
3. **Have direct backend access.** They can connect directly to databases or read file systems.

 In the Next.js App Router, every component is a **Server Component by default**. That's true for both layouts and pages. To make it a Client Component, you must add the directive `"use client"` at the very top of the file.

does that mean server data is exclusively to Server Components? can Client ones access it?

**Directly? No.**  
Client Components run in the user's browser (after being pre-rendered on the server). They cannot reach into your database or read the incoming HTTP request headers directly because they are running on the user's laptop, not your server.

**Indirectly? Yes.**  
They access server data by:
1. **Props:** A Server Component fetches data and passes it down to the Client Component as props.
2. **API Routes / Server Actions:** The Client Component makes an AJAX request (fetch) to your server to ask for data.

if we think of Server Components as the "skeleton" and Client Components as "the muscles", the picture gets solid clean. the skeleton is built for the muscles to give movement (using) it.

| Feature                | **Server Component** (Default)                       | **Client Component** (`"use client"`)                |
| :--------------------- | :--------------------------------------------------- | :--------------------------------------------------- |
| **Where it runs**      | Server only.                                         | Server (pre-render) + Browser.                       |
| **Access to Database** | ✅ Direct access.                                     | ❌ No. Must ask server via API.                       |
| **Access to Cookies**  | ✅ Can read incoming cookies.                         | ❌ Can only read `document.cookie` (if not HttpOnly). |
| **Interactivity**      | ❌ No `onClick`, `onChange`, `useState`, `useEffect`. | ✅ Yes. All React hooks work here.                    |
| **Bundle Size**        | 0kb (Code stays on server).                          | Adds to the JavaScript downloaded by user.           |
## TLDR;
**Use a Server Component when:**
- You need to fetch data (from DB, API, or Supabase).
- You need to access backend resources (API keys you don't want to expose).
- You are rendering static content (text, images, layout).