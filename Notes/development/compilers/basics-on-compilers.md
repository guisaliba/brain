Compilers do three main things:
1. Parsing
2. Transformation
3. Code generation

## Parsing
The parsing is typically divided into two parts:
1. Lexical Analysis: 
	Takes the raw code and starts splitting it into small pieces called **tokens**, this is done by a tokenizer or lexer. Tokens are an array of tiny objects that represents what is written in the source code, they usually have a `type` and a `value` and can be letters, numbers, parenthesis, brackets, punctuations, whatever. The tokenizer will generate a lot of tokens from the source code even if they are not correctly written, because it does not concern about syntax, only on generating tokens.

2. Syntactic Analysis
	Takes the generated tokens and transforms them into a more comprehensive structure, that is called an **Intermediate Representation** (IR) commonly being ASTs. For short, ASTs are deeply nested objects that represents code in an easier to understand way.

For the following syntax:
```
(add (subtract 4 2))
```

Tokens might look like this:
```
[
 { type: 'paren',  value: '('        },
 { type: 'name',   value: 'add'      },
 { type: 'number', value: '2'        },
 { type: 'paren',  value: '('        },
 { type: 'name',   value: 'subtract' },
 { type: 'number', value: '4'        },
 { type: 'number', value: '2'        },
 { type: 'paren',  value: ')'        },
 { type: 'paren',  value: ')'        },
]
```

And an AST for these produced tokens might look like this:
```
{
 type: 'Program',
 body: [{
        type: 'CallExpression',
        name: 'add',
        params: [{
          type: 'NumberLiteral',
          value: '2',
        }, {
          type: 'CallExpression',
          name: 'subtract',
          params: [{
            type: 'NumberLiteral',
            value: '4',
          }, {
            type: 'NumberLiteral',
            value: '2',
          }]
        }]
      }]
    }
```

Each of these `type, value` objects are known as **AST Node**.
We can have a Node for `NumberLiteral` and a Node for `CallExpression` just like this:

```
{
	type: 'NumberLiteral',
	value: '2',
}

{
	type: 'CallExpression',
	name: 'subtract',
	params: [...]
}
```

When transforming the AST we can add more nodes, remove existing ones, replace them or we can even leave the existing AST as it is and generate an entirely new one based on it. Since a compiler usually targets to compile code to another language, that's what we're going to do.
