---
title: What is 2>&1 and 2>/dev/null in Linux shells
source: https://www.perplexity.ai/search/what-is-2-1-and-2-dev-null-on-XluCGqfmTbyxJxfX4oq7eg
author:
published:
created: 2026-02-09
description: What some redirectors and processes standard streams do in Linux
tags:
---
In Linux shells, `2>&1` and `2>/dev/null` are redirection operators that control where a command sends its error messages. They work with the standard file descriptors: `0` (stdin), `1` (stdout), and `2` (stderr).

## Basics of file descriptors
- Every process has three standard streams: input (`0`), output (`1`), and error (`2`).
- `>` redirects standard output (`1`) unless you specify another descriptor number before it.
- Writing `2>` means “redirect file descriptor 2 (stderr) somewhere”.

## What 2>/dev/null does
- `/dev/null` is a special device that discards anything written to it (a “black hole”).
- `2>/dev/null` means “send stderr (file descriptor 2) to `/dev/null` ”, effectively hiding all error messages from that command.

Example:

```
bash
cmd 2>/dev/null
```

- Normal output (stdout) still appears.
- Only errors are suppressed.

## What 2>&1 does
- `&1` means “the same place file descriptor 1 (stdout) is currently going”, not a file named `1`.
- `2>&1` means “redirect stderr (2) to wherever stdout (1) is currently redirected”.

Examples:

```
bash
cmd >out.log 2>&1
```

- First, `>out.log` sends stdout to `out.log`.
- Then, `2>&1` sends stderr to the same place as stdout, so both stdout and stderr go into `out.log`.

```
bash
cmd >/dev/null 2>&1
```

- Stdout is redirected to `/dev/null`.
- Then stderr is redirected to “where stdout is”, which is `/dev/null`.
- Result: both normal output and errors are discarded.

## Order matters
These two are different:

```
bash
cmd >/dev/null 2>&1   # both stdout and stderr discarded
cmd 2>&1 >/dev/null   # stderr goes to original stdout; stdout goes to /dev/null
```

In the second case, stderr still appears on the terminal because it was redirected to stdout *before* stdout was changed.