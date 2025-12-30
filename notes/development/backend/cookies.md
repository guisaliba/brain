# subject: [[backend]]
## topics: #http #client-server #requests
--- 
in a regular HTTP flow, cookies are set in this sequence:
1. **Browser (Client) -> Server:** The browser sends a request. It includes the `Cookie` header (containing tokens).
2. **Server:** Reads the `Cookie` header. It processes the request.
3. **Server -> Browser (Client):** The server sends a response. If it wants to save/update a cookie, it includes the `Set-Cookie` header.