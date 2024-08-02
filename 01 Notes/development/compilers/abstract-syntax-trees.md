## How can a language recognize and understand exactly what a particular method or variable written in another language means in its own vocabulary?

This is made possible through **Abstract Syntax Trees (AST)**. ASTs are simply the representation of a particular code in a particular language in the form of a data structure (a tree). As a data structure, they can be represented in various formats, commonly as JSON.

When the conversion from source code to an AST occurs, only the structural content of the code is preserved; any other additional information is discarded. This means that in the end, we only have a tree containing the structural parts of the code written in that language, thus having the "base" of the language.

From this, it is possible to implement in another language an agent or entity capable of reading this data structure and interpreting the information present for its own vocabulary, methods, and actions.

In ASTs, each node of the tree represents a **construct**, a feature of the source code (of the original language), and in these nodes, we can find methods or representations belonging to that construct.

**An AST can be used by a compiler or an interpreter to translate (transpile) the structural content of the source code into another language.** In this way, we can compile or interpret any programming language into another.

[[parsing-and-lexing]].