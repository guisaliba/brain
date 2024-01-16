Some simple compilers basically mix lexical analysis, static analysis and code generating and produces an output for the code right in the parser without ever transforming it to an AST or other IRs. These are called **single-pass compilers** and they restrict the design of the language a lot.

Since you have no data structures for the source code it means that once you traverse the code you need to know enough of it to compile it. Languages like C and Pascal were designed like this. At the time, memory was so precious that a compiler couldn't store the source code for the program it was trying to compile, much less IRs of it.

## Tree-walk interpreters
Some programming languages begin executing code right after generating (parsing) the AST for the source code. They do that by traversing the three each branch and leaf evaluating every node it traverse.

This is very common to small languages like student projects but it's not widely used for general purposed languages. Many call these implementations as **interpreters** but that name is much more generally, so calling them tree-walk interpreters seems to fit better.

## Transpilers
What if you treated another source language as if it were an IR? Instead of doing all the work to lower the level of the language until it is interpretable by a machine, you would produce a string of valide source code for another language as high level as yours. People used to call this **source-to-source compiler** or **transcompiler** but nowadays, it is just **transpiler**.

That's why almost every language has a compiler that targets JavaScript, since JavaScript is the common way to run code in browsers, most languages started to make compilers that read source code and target JavaScript, hence, they can be called a **transpiler**.

The **TypeScript** compiler is one of the most famous examples of that. It is a very similar to JavaScript language that it's compiler read the code and compiles it to JS language. In this case, many phases of analysis may be skipped entirely and go straight for the output syntax in the destination language, in this case, JS.

## Just-in-Time Compilation
The fastest way to execute code is by compiling it to machine code, but you might not know what architecture your end user’s machine supports. Then what? You can do what JVM, .NET CLR and most JavaScript interpreters do: when the program is loaded on the target machine, you compile it to native code for the architecture their computer supports.

This is called **Just-in-Time** compilation or just **JIT**. There are other compilation ways they are better explained here: [[aot-jit-and-transpilers]].