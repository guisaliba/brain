Compilers can be made out of three types: **AOT, JIT, and Transpilers**. 

## Ahead-of-Time (AOT) compilers
The **AOT compiler (Ahead-of-Time)** does ahead of time translation. It means that the compilation (static time) is done before the execution time (runtime). In this case, the compiler produces a bunch of **Intermediate Representations (IR)** and then produces the native code (x64/x86). Here, the CPU will work as an interpreter, reading the machine code (native code) produced by the compiler and executing it.


## Just-in-Time (JIT) compilers
**JIT compilers (Just-In-Time)** on the other hand does the compilation at the same time it executes it. The purpose of them is to improve performance. They can produce, for example, native code for a huge function once and then when that function is called again and again in the code, it uses the cached native representations of it so it doesn't need to produce the native code for it every time the function is called.


## Transpilers
The last one is the **Transpiler**, or also called **AST transformers**. They transform **an AST into another AST**. It can be the transformation of the same language (JavaScript  to older versions of JavaScript), or from one language to another (C++ to Java, Python to JavaScript, etc.)

Asking if JavaScript, Python, C++, etc. are interpreted or compiled languages is the wrong question. What's interpreted or compiled are the implementations, not the language itself.

A language can have multiple ways to be handled. It can be compiled or interpreted using an AST interpreter, Bytecode interpreter, AOT compiler, JIT compiler, or  a transpiler. What really matters is if the runtime semantics are preserved.