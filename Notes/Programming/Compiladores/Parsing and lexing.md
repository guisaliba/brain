## The mountain

The network of paths of implementing a language is similar to climbing a mountain.
You start off at the bottom with the program as raw source text, literally just a string of characters. Each phase analyzes the program and transforms it to some higher-level representation where the semantics—what the author wants the computer to do—become more apparent.

We transform this highest-level representation down to successively lower-level forms to get closer and closer to something we know how to make the CPU actually execute.

This journey begins with the bare text (raw) of the user's source code:

```
p r i n t ( " h e l l o " )
```

That's it. This is a raw source code and we don't know what to do with it yet.

## Scanning
The first step is scanning, also known as **lexing**. A scanner, or **lexer**, takes a linear stream of characters and chunks them together into a series of something more akin to “words”.
These are called **tokens**, and because of that, a lexer can be also called a **tokenizer**.

Some characters in a source file don’t actually mean anything. Whitespace is often insignificant, and comments, by definition, are ignored by the language. The lexer usually discards these, leaving a clean sequence of meaningful tokens, like this one:

```
print ("hello")
```

**Tokens are usually an object** composed of two parts: **a type and a value**. For this example, we have two tokens. The first one `ID: "print"` can be read as `{ type: ID, value: "print" }` and the second one `String: "hello"` is the same as `{ type: String, value: "hello" }`.

Right now, the tokenizer (lexer) doesn't care about the syntax so it doesn't matter if it is correct or not. The only thing he's doing right now is generating tokens from the source code. Let's take a look to another example:

```
if (
```

This is a broken syntax, because the compiler expects a condition inside the opened parenthesis. It also expects a closing parenthesis after the condition. But here, the lexer will read it and produce tokens with no problems since it won't check for syntax right now.

The tokens produced from this would be: `keyword: "if" -> type: keyword, value: "if"` and `op: "(" -> type: op - open parenthesis, value: "("`. 

## Parsing
Now the parser handles the **syntax analysis**, where our syntax gets a **grammar**. This phase is also called **syntactic analysis**. A parser takes the sequence of tokens and joins them together to form what is called a tree structure. These trees have a couple different names (based on how close they are to the syntactic structure of the source language). 

Usually, they are called **syntax trees**, [[Abstract Syntax Trees (ASTs)]] or just **trees**. It is important to notice that this is still happening at static time and not at runtime. The only thing parser does here is reading the produced tokens and generating an AST from them.

Programming languages are much simpler than human languages. Giving them a grammar is much easier to do. Sometimes we still make some mistakes and one of the parser's jobs is to tell us that we wrote something wrong by reporting **syntax errors**.

**Runtime semantics**
What is runtime semantics? It is the study of the meaning of the program. In other words, it is the analysis of questions like: **What does it mean to define a variable? What is a function? How does scope works? How do you pass parameters? What's a call stack?** and semantics can be different for different programming languages.

A clear example for that is the comparison on variable scope for JavaScript and PHP. While in JavaScript, if you define a variable outside of a function that function will still "see" the defined variable, in PHP that same function would not know that same variable. 

This behavior is due to all functions being closures in JavaScript, so they keep the parent environment so they can reuse all values defined outside them while in PHP that doesn't happen:

``` js
const data = "JS";

function printData() {
	console.log(data);
}

printData(); // JS
```

``` php
$data = "PHP";

function printData() {
	print($data);
}

printData() // Undefined variable: data
```

