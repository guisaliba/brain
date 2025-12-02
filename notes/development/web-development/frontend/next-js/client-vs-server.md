# subject: [[next-js]]
## topics: #nextjs #server-components #client-components
 --- 
 By default, layouts and pages are [Server Components](https://react.dev/reference/rsc/server-components), which lets you fetch data and render parts of your UI on the server, optionally cache the result, and stream it to the client. When you need interactivity or browser APIs, you can use [Client Components](https://react.dev/reference/rsc/use-client) to layer in functionality.

## When to use server and client components?

Use **Client Components** when you need:
- [State](https://react.dev/learn/managing-state) and [event handlers](https://react.dev/learn/responding-to-events)- . E.g. `onClick`, `onChange`
- [Lifecycle logic](https://react.dev/learn/lifecycle-of-reactive-effects), e.g.: `useEffect`
- Browser-only APIs, e.g.: `localStorage`, `window`, `Navigator.geolocation`, etc.
- [Custom hooks](https://react.dev/learn/reusing-logic-with-custom-hooks)

Use **Server Components** when you need:
- Fetch data from databases or APIs close to the source.
- Use API keys, tokens, and other secrets without exposing them to the client.
- Reduce the amount of JavaScript sent to the browser.
- Improve the [First Contentful Paint (FCP)](https://web.dev/fcp/) , and stream content progressively to the client.

The component below `<Page>` is clearly a Server Component, since it **fetches data** and passes it as props to the `<LikeButton>` component. `<LikeButton>` is a Client Component.

```tsx
import LikeButton from '@/app/ui/like-button'
import { getPost } from '@/lib/data'
 
export default async function Page({
  params,
}: {
  params: Promise<{ id: string }>
}) {
  const { id } = await params
  const post = await getPost(id) // Fetches data about the post
 
  return (
    <div>
      <main>
        <h1>{post.title}</h1>
        {/* ... */}
        <LikeButton likes={post.likes} />
      </main>
    </div>
  )
}
```

```tsx
'use client' // -> Strictly says "this component as a Client Component"
 
import { useState } from 'react'
 
export default function LikeButton({ likes }: { likes: number }) {
  // ...
}
```

`<LikeButton>` handles client-side interactivity (counts the number of likes on a post).

`"use client"` is used to declare a **boundary** between the Server and Client module graphs (trees).

Once a file is marked with `"use client"`, **all its imports and child components are considered part of the client bundle**. This means you don't need to add the directive to every component that is intended for the client.

## How do Server and Client components work?
### On the server
- **Server Components** are rendered into a special data format called the React Server Component Payload (RSC Payload).
- **Client Components** and the RSC Payload are used to [pre-render](https://nextjs.org/docs/app/guides/caching#rendering-strategies) HTML.

> **What is the React Server Component Payload (RSC)?**
> 
> The RSC Payload is a compact binary representation of the rendered React Server Components tree. It's used by React on the client to update the browser's DOM. The RSC Payload contains:
> 
> - The rendered result of Server Components
> - Placeholders for where Client Components should be rendered and references to their JavaScript files
> - Any props passed from a Server Component to a Client Component

### On the client (first rendering)
1. **HTML** is used to immediately show a fast non-interactive preview of the route to the user.
2. **RSC Payload** is used to reconcile the Client and Server Component trees.
3. **JavaScript** is used to hydrate Client Components and make the application interactive.

> **What is hydration?**
> Hydration is React's process for attaching [event handlers](https://react.dev/learn/responding-to-events) to the DOM, to make the static HTML interactive.