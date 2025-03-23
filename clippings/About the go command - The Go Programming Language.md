---
title: "About the go command - The Go Programming Language"
source: "https://go.dev/doc/articles/go_command"
author:
published:
created: 2025-03-23
description:
tags:
  - "clippings"
---
The Go distribution includes a command, named "`[go](https://go.dev/cmd/go/)`", that automates the downloading, building, installation, and testing of Go packages and commands.

## Go's conventions¶

The `go` command requires that code adheres to a few key, well-established conventions.

First, the import path is derived in a known way from the URL of the source code. For Bitbucket, GitHub, Google Code, and Launchpad, the root directory of the repository is identified by the repository's main URL, without the `https://` prefix. Subdirectories are named by adding to that path. For example, the source code of the Google logging package `glog` is obtained by running

```
git clone https://github.com/golang/glog
```
and thus the import path of the [glog](https://pkg.go.dev/github.com/golang/glog) package is "`github.com/golang/glog`".

These paths are on the long side, but in exchange we get an automatically managed name space for import paths and the ability for a tool like the go command to look at an unfamiliar import path and deduce where to obtain the source code.

Second, the place to store sources in the local file system is derived in a known way from the import path, specifically `$GOPATH/src/<import-path>`. If unset, `$GOPATH` defaults to a subdirectory named `go` in the user's home directory. If `$GOPATH` is set to a list of paths, the go command tries `<dir>/src/<import-path>` for each of the directories in that list.

Each of those trees contains, by convention, a top-level directory named "`bin`", for holding compiled executables, and a top-level directory named "`pkg`", for holding compiled packages that can be imported, and the "`src`" directory, for holding package source files. Imposing this structure lets us keep each of these directory trees self-contained: the compiled form and the sources are always near each other.

Third, each directory in a source tree corresponds to a single package. By restricting a directory to a single package, we don't have to create hybrid import paths that specify first the directory and then the package within that directory. Also, most file management tools and UIs work on directories as fundamental units. Tying the fundamental Go unit—the package—to file system structure means that file system tools become Go package tools. Copying, moving, or deleting a package corresponds to copying, moving, or deleting a directory.

Fourth, each package is built using only the information present in the source files. This makes it much more likely that the tool will be able to adapt to changing build environments and conditions. For example, if we allowed extra configuration such as compiler flags or command line recipes, then that configuration would need to be updated each time the build tools changed; it would also be inherently tied to the use of a specific toolchain.

## Getting started with the go command¶

Finally, a quick tour of how to use the go command. As mentioned above, the default `$GOPATH` on Unix is `$HOME/go`. We'll store our programs there. To use a different location, you can set `$GOPATH`; see [How to Write Go Code](https://go.dev/doc/code.html) for details.

We first add some source code. Suppose we want to use the indexing library from the codesearch project along with a left-leaning red-black tree. We can install both with the "`go get`" subcommand:

```
$ go get github.com/google/codesearch/index
$ go get github.com/petar/GoLLRB/llrb
$
```

Both of these projects are now downloaded and installed into `$HOME/go`, which contains the two directories `src/github.com/google/codesearch/index/` and `src/github.com/petar/GoLLRB/llrb/`, along with the compiled packages (in `pkg/`) for those libraries and their dependencies.

Because we used version control systems (Mercurial and Git) to check out the sources, the source tree also contains the other files in the corresponding repositories, such as related packages. The "`go list`" subcommand lists the import paths corresponding to its arguments, and the pattern "`./...`" means start in the current directory ("`./`") and find all packages below that directory ("`...`"):

```
$ cd $HOME/go/src
$ go list ./...
github.com/google/codesearch/cmd/cgrep
github.com/google/codesearch/cmd/cindex
github.com/google/codesearch/cmd/csearch
github.com/google/codesearch/index
github.com/google/codesearch/regexp
github.com/google/codesearch/sparse
github.com/petar/GoLLRB/example
github.com/petar/GoLLRB/llrb
$
```

We can also test those packages:

```
$ go test ./...
?   	github.com/google/codesearch/cmd/cgrep	[no test files]
?   	github.com/google/codesearch/cmd/cindex	[no test files]
?   	github.com/google/codesearch/cmd/csearch	[no test files]
ok  	github.com/google/codesearch/index	0.203s
ok  	github.com/google/codesearch/regexp	0.017s
?   	github.com/google/codesearch/sparse	[no test files]
?       github.com/petar/GoLLRB/example          [no test files]
ok      github.com/petar/GoLLRB/llrb             0.231s
$
```

If a go subcommand is invoked with no paths listed, it operates on the current directory:

```
$ cd github.com/google/codesearch/regexp
$ go list
github.com/google/codesearch/regexp
$ go test -v
=== RUN   TestNstateEnc
--- PASS: TestNstateEnc (0.00s)
=== RUN   TestMatch
--- PASS: TestMatch (0.00s)
=== RUN   TestGrep
--- PASS: TestGrep (0.00s)
PASS
ok  	github.com/google/codesearch/regexp	0.018s
$ go install
$
```

That "`go install`" subcommand installs the latest copy of the package into the pkg directory. Because the go command can analyze the dependency graph, "`go install`" also installs any packages that this package imports but that are out of date, recursively.

Notice that "`go install`" was able to determine the name of the import path for the package in the current directory, because of the convention for directory naming. It would be a little more convenient if we could pick the name of the directory where we kept source code, and we probably wouldn't pick such a long name, but that ability would require additional configuration and complexity in the tool. Typing an extra directory name or two is a small price to pay for the increased simplicity and power.