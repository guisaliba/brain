compilers are a crucial implementations of programming languages that do three main things: parse the source code, transform it and generate code from source.
## parsing
The parsing is typically divided into two parts:
### 1. Lexical Analysis
Takes the raw code and starts splitting it into small pieces called **tokens** and this is done by a tokenizer or **lexer**. Tokens are an array of tiny objects that represents what is written in the source code, they usually have a `type` and a `value` and can be letters, numbers, parenthesis, brackets, punctuations, whatever. The tokenizer will generate a lot of tokens from the source code even if they are not correctly written, because it does not concern about syntax, only on generating tokens.
### 2. Syntactic Analysis
Takes the generated tokens and transforms them into a more comprehensive structure, that is called an **Intermediate Representation** (IR) commonly being ASTs. For short, ASTs are deeply nested objects that represents code in an easier to understand way.
## transformation

## code generation