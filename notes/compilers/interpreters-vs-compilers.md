**Compiling** is an _implementation technique_ that involves translating a source language to some other—usually lower-level—form. When you generate bytecode or machine code, you are compiling. When you transpile to another high-level language, you are compiling too.

When we say a language implementation “is a **compiler**”, we mean it translates source code to some other form but doesn’t execute it. The user (usually some kind of builder/runner of the language) has to take the resulting output and run it themselves. Conversely, when we say an implementation “is an **interpreter**”, we mean it takes in source code and executes it immediately. It runs programs “from source”.

![[Pasted image 20230918005920.png]]
If you have a program and needs the output for that program, you need an interpreter. For interpreted languages like JavaScript, the interpreter interprets the code and gets the output for it. The compiler would translate that same program (p1) to another one (p2) and then, call some sort of interpreter for p2 to handle it and give the expected output.

If the compiler converts the program into machine code (x64/x86), then the interpreter for this converted program can be the **CPU**, because it would be able to understand and execute it. The CPU acts just like an interpreter running the (machine) code and getting the output. Languages like C++ do that kind of thing.

## AST Interpreters and VMs

**AST**-based interpreters use a **tree data structure** to represent the source code. Bytecode-based interpreters (**VMs**) have an extra step called **bytecode emitter** where it generates bytecode representations and then interpret this generated format.

VMs are optimized for storage and traversing, because bytecodes are just a plain array of bytes, taking less space and being easier to traverse than a tree data structure.

### The two types of VMs are:
- Stack-based machines
    - Stack for operands and operators;
    - The result is on top of the stack;

- Register-based machines
    - Set of virtual registers;
    - A register is a data storage;
    - The result is in an accumulator register;
    - Mapped to real (physical) registers on the machine;

There are different ways to represent ASTs. Take this code for example:
```
x = 15;
x + 10 - 5;
```

A possible representation for the AST of this code is to use "objects", like this:
![[Pasted image 20230918011841.png]]
This AST can be understood as this:
- The whole structure is a program with a list of statements
- The first statement is an assignment expression
    - The left side of the assignment is the identifier `x`
    - The right side of the assignment is the literal `15`
- The second statement is a binary expression, an operation
    - The binary expression is a subtraction operation (the operator is `-`)
    - The left side is another binary expression
        - It's an addition operation, it sums the identifier `x` with the literal `10`
    - The right side is a literal, `5`

But there is another way to represent this AST: using arrays. The first position of the array would be the statement (`assign, add, sub`), the second position would be the left side of the three and the third position would be the right side of it.
![[Pasted image 20230918012049.png]]
In this case:
- We have the program
- The first statement/expression
    - 1st position: `assign` type
    - 2nd position: `x` identifier (left child)
    - 3rd position: `15` literal (right child)
- The second statement/expression
    - 1st position: `sub` type
    - 2nd position: a new node (left child)
        - 1st position: `add` type
        - 2nd position: `x` identifier (left child)
        - 3rd position: `10` literal (right child)
    - 3rd position: `5` literal (right child)

Arrays are just an easier way to visualize the tree, both here represent the same thing.