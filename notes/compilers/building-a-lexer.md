**Lexing** is the process of transforming raw source code into tokens.

This transformation is done by the tokenizer, also called the scanner or lexer, hence the name lexing. A lexer reads source code and produces tokens out of it, even if what they read is syntactically incorrect, because they don't validate syntax and don't even know what is the syntax for the source code they're tokenizing.

`let x = 5 + 5;`

A token produced by the lexing of this code might be:

```
[
	LET,
	IDENTIFIER('x'),
	EQUAL_SIGN,
	INTEGER(5),
	PLUS_SIGN,
	INTEGER(5),
	SEMICOLON,
]
```

Notice that we don't count whitespaces as tokens, and comments are ignored by nature.

## Defining a token
To define tokens, we may create a class to represent and create them once we start analyzing our code. Remember that classes are complex data structures that can be created and implemented in code.

``` ts
export type TokenType = string;

export class Token {
	type: TokenType;
	literal: string;

	constructor(type: TokenType, literal: string) {
		this.type = type;
		this.literal = literal;
	}
}
```

The implementation of a token, that is, an instantiation of that class is very simple: it should contain a type and a literal. A simple example for that would be creating a token for the basic operator `+`.

``` ts
const plusToken = new Token('PLUS', '+')
```

Its type is `PLUS` and its literal `+`. From that we can define every possible type of tokens:

``` ts
export enum Tokens {
  ILLEGAL = 'ILLEGAL',
  EOF = 'EOF',
  IDENT = 'IDENT',
  INT = 'INT',
  ASSIGN = '=',
  PLUS = '+',
  COMMA = ',',
  SEMICOLON = ';',
  LPAREN = '(',
  RPAREN = ')',
  LBRACE = '{',
  RBRACE = '}',
  FUNCTION = 'FUNCTION',
  LET = 'LET',
}
```

Now, instead of using a random string we can use one of these to create a token:

``` ts
const letToken = new Token(Token.LET, 'LET');
```

## Lexer
The lexer, as already mentioned, is the one responsible for generating tokens. It is also called a tokenizer because of its job. We can now use our lexer to receive the source code input and output each token while reading the source code.

In order to do that, our Lexer needs to be validated which means each token it generates should correctly match what these tokens are, if it generates a token `+` for example that does not match the `Token.PLUS` it is not working as intended. We'll add tests to do that:

``` ts
import { Token, Tokens } from 'src/token/token';
import { Lexer } from '../lexer';

describe('lexer' () => {
	it ('matches each token', () => {
		const input = '=+,(){};'
		const tokens: Token[] = [
			{ type: Tokens.ASSIGN, literal: '=' },
			{ type: Tokens.PLUS, literal: '+' },
			{ type: Tokens.COMMA, literal: ',' },
			{ type: Tokens.LPAREN, literal: '()' },
			{ type: Tokens.RPAREN, literal: ')' },
			{ type: Tokens.LBRACE, literal: '{' },
			{ type: Tokens.RBRACE, literal: '}' },
			{ type: Tokens.SEMICOLON, literal: ';' },
		];

		const lexer = new Lexer(input);
		tokens.forEach(({ type, literal }) => {
			conts inputToken = lexer.nextToken();
			expect(inputToken.type).toEqual(type);
			expect(inputToken.literal).toEqual(literal);
		});
	});
})
```

Let's break it down:
-  `input` is the source code the lexer reads.
-  `tokens` is a list of `Token` we expect to match the source code.
-  `Lexer` is a class to be implemented yet.
	-  It receives an input as source code.
	-  And have a `nextToken` method to output the next token.

Running this would result in an error since the `Lexer` hasn't been implemented yet so that's the next thing to do. To help us analyze the code, we'll have 4 different helpers:

-  `input`: the actual source code.
-  `position`: the current position of the current char we are reading.
-  `readPosition`: the position we are about to read the next char.
-  `char`: the character of the source code we are reading.

With these we can build our class `Lexer`.

``` ts
export class Lexer {
	input: string;
	position: number;
	readPosition: number;
	char: string;

	constructor(input: string) {
		this.input = input;
	}
}
```

We now fix the implementation of the Lexer class but we still don't have the `nextToken()` method which will result in another error if we try to run this code. Let's implement it then:

``` ts
export class Lexer {
	input: string;
	position: number;
	readPosition: number;
	char: string;
	
	INITIAL_POSITION = 0;
	EMPTY_CHAR = '';
	
	constructor(input: string) {
		this.input = input;
		this.setUpInitialState();
	}

	private setUpInitialState() {
		this.position = this.INITIAL_POSITION;
		this.readPosition = this.INITIAL_POSITION;
		this.char = this.EMPTY_CHAR;
	}
}
```

The `nextToken` algorithm is simple: it just needs to read the next character, transform this character into a token then return this new produced token. Let us implement it:

``` ts
export class Lexer {
	input: string;
	position: number;
	readPosition: number;
	char: string;
	
	INITIAL_POSITION = 0;
	EMPTY_CHAR = '';
	
	constructor(input: string) {
		this.input = input;
		this.setUpInitialState();
	}
	
	private setUpInitialState() {
		this.position = this.INITIAL_POSITION;
		this.readPosition = this.INITIAL_POSITION;
		this.char = this.EMPTY_CHAR;
	}
	
	private readChar() {
		if (this.readPosition >= this.input.length) {
			this.char = '';
		} else {
			this.char = this.input[readPosition];
		}
		
		this.position = this.readPosition;
		this.readPosition += 1;
	}
}
```

We start verifying the `readPosition` to make sure that we didn't finish reading the entire source code. If we finish reading the source code, we just update the `char` with its initial state (empty string). To get the next character, we just access the input with the next position index and update the `char`.

After that, we always need to update the indices:

- `position` becomes the `readPosition`
- `readPosition` increments by one

Now we can generate tokens based on the current state of our character's position. We just need to map our current `char` to its own `Token` and we can achieve that with a simple `switch`:

```ts
private getToken(): Token {
  switch (this.char) {
    case '=':
      return new Token(Tokens.ASSIGN, '=');
    case ';':
      return new Token(Tokens.SEMICOLON, ';');
    case '(':
      return new Token(Tokens.LPAREN, '(');
    case ')':
      return new Token(Tokens.RPAREN, ')');
    case ',':
      return new Token(Tokens.COMMA, ',');
    case '+':
      return new Token(Tokens.PLUS, '+');
    case '{':
      return new Token(Tokens.LBRACE, '{');
    case '}':
      return new Token(Tokens.RBRACE, '}');
    case '':
      return new Token(Tokens.EOF, '');
  }
}
```

Getting everything together, we need to setup the lexer with the appropriate initial state and then start reading the source code. The constructor should look like this now:

``` ts
export class Lexer {
	input: string;
	position: number;
	readPosition: number;
	char: string;
	
	INITIAL_POSITION = 0;
	EMPTY_CHAR = '';
	
	constructor(input: string) {
		this.input = input;
		this.setUpInitialState();
		this.readChar();
	}
	
	private setUpInitialState() {
		this.position = this.INITIAL_POSITION;
		this.readPosition = this.INITIAL_POSITION;
		this.char = this.EMPTY_CHAR;
	}
	
	private readChar() {
		if (this.readPosition >= this.input.length) {
			this.char = '';
		} else {
			this.char = this.input[readPosition];
		}
		
		this.position = this.readPosition;
		this.readPosition += 1;
	}
	
	private getToken(): Token {
	  switch (this.char) {
	    case '=':
	      return new Token(Tokens.ASSIGN, '=');
	    case ';':
	      return new Token(Tokens.SEMICOLON, ';');
	    case '(':
	      return new Token(Tokens.LPAREN, '(');
	    case ')':
	      return new Token(Tokens.RPAREN, ')');
	    case ',':
	      return new Token(Tokens.COMMA, ',');
	    case '+':
	      return new Token(Tokens.PLUS, '+');
	    case '{':
	      return new Token(Tokens.LBRACE, '{');
	    case '}':
	      return new Token(Tokens.RBRACE, '}');
	    case '':
	      return new Token(Tokens.EOF, '');
	  }
	}
	
	private nextToken() {
		const token = this.getToken();
		this.readChar();
		return token;
	}
}
```

As we read the next character in the constructor of the `Lexer`, we get the token, read the next character and return the created token.

Running our test again, we fixed all the issues and it is passing now.