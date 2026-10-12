**Root** is a specific user account. On any Unix system it's the account with UID `0`, and the kernel gives UID 0 special treatment: permission checks are essentially skipped. It's a real account with an entry in `/etc/passwd`, a home directory (`/root` usually), etc.

**"Superuser"** isn't a separate account — it's a _role/concept_. It just means "a user with unrestricted privileges over the system." On Unix, the superuser role happens to be implemented as the root account. So in practice, "the superuser" and "root" are the same thing — root is just the name of the account that has superuser privileges. Some systems could theoretically implement fine-grained "superuser-like" capabilities without full root (e.g. Linux capabilities like `CAP_NET_BIND_SERVICE`), but colloquially "superuser" = root.

mental model: `superuser` is the interface; `root` implements `superuser` (on Unix systems).

**`su`** stands for "substitute user" (sometimes said as "switch user"). It lets you become another user, and if you don't give it a username, it defaults to root:

- `su` → asks for **root's password**, then gives you a root shell
- `su alice` → asks for **alice's password**, then gives you alice's shell

**`sudo`** stands for "superuser do." It runs a _single command_ as another user (root by default), authenticating with **your own password**, and only if `/etc/sudoers` says you're allowed to.

So `sudo su` means: "use sudo to run the `su` command, as root." Two things happen:

1. `sudo` checks you're allowed to run commands as root, asks for _your_ password.
2. It then executes `su` — running as root already, `su` with no args tries to become root, and since the process is already root, no password prompt is needed for that inner step.

End result: yes, you land in a root shell. It works, but it's a bit of a redundant combo — most people use `sudo -i` or `sudo -s` instead, which do the same "get me a root shell" job more directly without invoking `su` inside `sudo`. `sudo su` is especially common as a habit on systems like Ubuntu, where the root account's password is disabled by default — so plain `su` alone won't work there (no root password to authenticate with), but `sudo su` works fine because sudo authenticates you with your own password first.