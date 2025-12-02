# subject: [[pull-strategies]]
## topics: #git #branches
--- 
## 1. `pull.rebase = false` → **Merge**

**Name / concept:**
- “Pull with merge” (the classic behavior).
- Internally: `git pull` = `git fetch` + `git merge`.

**When branches are divergent:**
Imagine this history:

- Remote `origin/main`:
```text
A -- B -- C   (origin/main)
```

- Local `main`:
```text
A -- B -- D   (main)
```
You have **C** only on remote, and **D** only locally.

Running `git pull` with `pull.rebase = false` creates a **merge commit**:
```text
A -- B -- C ------- M   (origin/main after push)
           \      /
            D ----    (main after pull)
```
Where **M** is a new commit that has _two parents_ (C and D).

**Effect on local branch:**
- Local branch gets a **new merge commit**.
- You keep both lines of history intact (no rewriting of existing commits).
- Your old local commit hash **D** stays as-is.

**Effect on remote (after `git push`):**
- You push the merge commit **M**.
- Remote history now has **M** as the tip, with a visible merge.

**Pros:**
- Safe: no history rewriting of already pushed commits.
- Good for shared branches where you don’t want to rewrite history.

**Cons:**
- History can get noisy with a lot of merge commits, especially if everyone does this on feature branches.
## 2. `pull.rebase = true` → **Rebase**

**Name / concept:**
- “Pull with rebase”.
- Internally: `git pull --rebase` = `git fetch` + `git rebase`.

Same starting situation:

Remote:
```text
A -- B -- C   (origin/main)
```

Local:
```text
A -- B -- D   (main)
```

With **rebase**, Git **takes your local commits (D, etc.) and replays them on top of the updated remote history**:

After `git pull --rebase` locally:
```text
A -- B -- C -- D'   (main)
          ^
          origin/main (after fetch, before push)
```
- Note: **D'** is a _new_ commit (same content as D, different hash) rebased on top of C.

**Effect on local branch:**
- Your local branch is **rewritten** so that it looks like you committed after the remote commits.
- Original commits (D) are replaced by new ones (D', possibly D'', etc.).
- This rewrites history (changes commit hashes).

**Effect on remote (after `git push`):**
- You push the rebased commits, so the remote branch becomes:
```text
A -- B -- C -- D'   (origin/main, main)
```
- The history is **linear**, no merge commit.

**Pros:**
- Clean, linear history.
- Easier to read `git log`, bisect, etc.

**Cons:**
- You’re rewriting history. If those commits were already pushed and someone else based work on them, using rebase/push-force can screw them.
- Needs a bit more discipline (often used with `git push --force-with-lease` on feature branches, not on shared main branch).

## 3. `pull.ff = only` → **Fast-forward only**

**Name / concept:**
- “Fast-forward only pull”.
- Internally: `git pull --ff-only` = `git fetch` + try a **fast-forward merge**; if impossible → **error**.

Fast-forward merge means: “I can just move the branch pointer forward; no new commit, no rebase, nothing fancy.”

Example where it **is** possible:

Remote:
```text
A -- B -- C   (origin/main)
```

Local:
```text
A -- B        (main)
```

Here local is _behind_ remote, not divergent. Fast-forward is trivial:
```text
A -- B -- C   (main and origin/main)
```

But in  the case of a divergence:

Remote:
```text
A -- B -- C   (origin/main)
```

Local:
```text
A -- B -- D   (main)
```

There is **no** fast-forward: local has **D**, remote has **C**, they’re different lines.

With `pull.ff=only`, `git pull` will:
- **Refuse** to proceed and show an error.
- It won’t merge, won’t rebase, won’t touch your history.

**Effect on local branch:**
- Nothing changes when branches are divergent – you just get an error.

**Effect on remote (after push):**
- None either, because you never get to a successful pull and likely can’t push without doing something else.

**Pros:**
- Guarantees that your branch history stays linear without any implicit merges or rebases.
- Good if you want strict, “no automatic merging” rules.

**Cons:**
- Annoying when divergence happens: you must manually choose `merge` or `rebase` (or fix things another way) before you can proceed.

## What the git hint message tells you about divergent branches

> `hint: You have divergent branches and need to specify how to reconcile them.`

Translation:  
“Your local branch and the remote branch both have commits the other doesn’t. I don’t know if you want to resolve that with a **merge**, a **rebase**, or if you only want to allow **fast-forward** (which would fail right now). Pick a policy.”

Then it offers ways to set the **default behavior**:
- `git config pull.rebase false` → default to **merge**.
- `git config pull.rebase true` → default to **rebase**.
- `git config pull.ff only` → default to **fast-forward only**.

And it reminds you can:
- Use `--global` to set it for **all** repos.
- Override per command: `git pull --rebase`, `git pull --no-rebase`, `git pull --ff-only`.
## Practical rule of thumb
- For **shared main branch** on a team:
    - Many teams stick with **merge** or **ff-only** (with PRs doing merges on the server).
- For **your own feature branches**:
    - `pull.rebase = true` is usually nicer → clean linear history, then squash/merge via PR.