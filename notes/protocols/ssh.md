SSH (Secure Shell) is a **network** protocol and tool used to securely access and manage remote computers over an untrusted network like the internet. typical use is for remote shell access.

the unix command `ssh user@server` is the standard way to administer servers and network devices thorough the SSH protocol.

## flags
With `ssh`, `-L` is for local port forwarding, and `-fN` is a common combo to run that forwarding in the background without opening a remote shell.

### `-L` flag
the `-L` flag sets up a tunnel from a local port (or Unix socket) to a host/port (or socket) reachable from the remote side.
- Syntax examples:
    - `ssh -L 8080:localhost:80 user@server` forwards local port 8080 to port 80 on `localhost` from the server’s point of view.​
    - `ssh -L [bind_address:]port:host:hostport user@server` is the general TCP form.[
- Use it to access remote services (DBs, web servers, etc.) as if they were local, over an encrypted SSH tunnel.​

### `-f` and `-N` together
the `-f` and `-N` flags are often used together when doing port forwarding only.​
- `-N`
    - Tells `ssh` to not execute any remote command; it will just establish the connection and keep it open (useful for pure tunneling/forwarding).​
- `-f`
    - Puts `ssh` into the background after authentication, so the tunnel keeps running while your shell prompt returns.​

Typical pattern:

`ssh -fN -L 8080:localhost:80 user@server`

This:
- Opens an SSH connection to `server`.​
- Sets up local port 8080 → remote `localhost:80` forwarding.​
- Does not start a remote shell (`-N`).​
- Backgrounds itself after connecting (`-f`), leaving the tunnel running.​

`-L 7233:localhost:7233` means: “Listen on local port 7233, and whenever something connects to it, forward that traffic over SSH to `localhost:7233` as seen from the remote side.”
- So:
    - On your local machine: a listener is created on port 7233.​
    - On the remote server: SSH connects to `localhost:7233` there (often a service bound to 127.0.0.1:7233 that is _not_ exposed publicly).​        
    - Only clients on your local machine (or whatever can reach your local 7233, depending on bind address) can use this tunnel; random hosts on the internet cannot hit the remote’s port 7233 via this option alone.​
### Role of `-fN`
- `-N`: do not run a remote command; just keep the connection open for forwarding.
- `-f`: go to background after authentication, so the tunnel stays up while your shell returns.​

If you wanted to “open” a local service to the remote side, you would instead use `-R` (remote port forwarding), e.g. `ssh -R 7233:localhost:7233 user@remote`.​