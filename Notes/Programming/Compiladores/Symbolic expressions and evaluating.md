Take a look at this expression:
`total = current + 150;`

It is a simple addition expression right? We are basically assigning this addition to the identifier `total`, which is probably a variable declared somewhere in the code. We can represent this expression with an AST, it should look like this:

```
{
  type: "Assignment",
  left: {
    type: "Identifier",
    value: "total"
  },
  right: {
    type: "Addition",
    left: {
      type: "Identifier",
      value: "current"
    },
    right: {
      type: "Literal",
      value: 150
    }
  }
}
```

It begins with `type: "Assignment"` which is the operation our expression is doing: assigning a value to the `total` identifier. Then, our tree has two children: **left and right**, where the left children is the `total` identifier and the right side is another expression, an addition `current + 150`. Since the right side is another operation, we declare its type as 
an `Addition`, in which its left side is represented by the `current` identifier and its right side is the number (literal) `150`. This way we represent that single line of code in an AST.

But what if instead of the words `type, left, right` we used numbers like `0, 1, 2`? Well, that's completely ok, we can do that by saying type, left and right will now be represented by 0, 1 and 2 respectively, just like this:

- `type`: 0
- `left`: 1
- `right`: 2

Then if we go back to our AST, we can change it to our new format:
```
{
  0: "Assignment",
  1: {
    0: "Identifier",
    value: "total"
  },
  2: {
    0: "Addition",
    1: {
      0: "Identifier",
      value: "current"
    },
    2: {
      0: "Literal",
      value: 150
    }
  }
}
```

Notice that since we have numbers representing these guys, they can be used as indexes and since they are part of a tree data structure, we can access them through their indexes. This feels just like an array, right? Yes, that's exactly what it is supposed to be, we are transforming this structure from an object to an array.

```
[
  'Assignment',
  ['Identifier', 'total'],
  ['Addition', ['Identifier', 'current'], ['Literal', 150]],
];
```

Now if we want to access the literal `150` for example, we could do that by doing so
```
tree[2][2][1] // 150
```

Because `150` is located at `index[2]`, in the third position `index[2][2]` and in the second position of that one `index[2][2][1]`. To simplify even more, we can transform the operators (Assignment, Addition, Identifier, Literal, etc) into actual symbols:

- `Assignment` → `set`
- `Identifier: total` → `total`
- `Addition` → `+`
- `Identifier: current` → `current`
- `Literal: 150` → `150`

We would end up with something like this:
```
[
  'set', // type tag
  'total', // left hand side
  [
    '+', // type tag
    'current', // left hand side
    150, // right hand side
  ], // right hand side
];
```

This is called **S-expression** or **Symbolic expressions**. This way we don't need a parser here, since it is just a list of lists (an array of arrays), we can use JavaScript to interpret the source code.

## Eva
Let's say we have a programming language and it's name is **Eva**. It will be responsible to interpret and evaluate expressions. And this could be done by any other programming language like JavaScript, Java, C#, etc we just want it to be Eva right now.

Here are some examples of the language syntax:

### Addition:
`(+ 5 10) // 15`
The type is the symbol `+` and it has two operands, in this case `5` and `10`.

### Assignment:
`(set x 15) // 15`
The type is `set`, an assignment if you remember, and it is assigning the value `15` to the variable `x` which is an already declared variable in our code. It also **produces a value** for that assignment which in this case is 15.

### The if expression:
``` Eva
(if (> x 10)
	(print "ok)
	(print "err))
```

### Functions:
``` Eva
(def foo (bar)
	(+ bar 10))
```
It is important to say that all functions in the Eva programming language are **closures**.

### Lambda expression / anonymous function:
``` Eva
// IILE - immediately-invoked lambda expression
(lambda (x) (* x x) 10) // 100
```
They are very very similar to arrow functions in JavaScript.

In the Eva language, there is a little difference between **statements** and **expressions**: while statements don't produce any value from a given operation, expressions always produce a value. And that's it.

The `Eva` class will be responsible to represent the Eva programming language. Notice that even though it is a JavaScript class, the responsible for interpreting and evaluating expressions a given source code will be the `Eva` class. This means we'll have to implement every kind of evaluation and interpretation on it:

``` JavaScript
class Eva {
	eval(exp) {
		throw 'Unimplemented';
	}
}
```

Here, the `eval()` method evaluates an input and returns a response for that evaluation. Since we haven't implemented any evaluation, if we call it and pass any expression to it, we'll get `Unimplemented` as a resolve.

``` JavaScript
const assert = require('assert');
const eva = new Eva();

assert.strictEqual(eva.eval(1), 1); // Unimplemented
```

In this example, we tried to evaluate through `Eva` if the number `1` is strictly equals to `1`. We used the method `strictEqual()` from JavaScript to help us on that. And as expected, it resolved on `Unimplemented`, since we didn't implement that evaluation yet. Let's do it:

``` JavaScript
class Eva {
  eval(exp) {
    if (isNumber(exp)) {
      return exp;
    }

    throw 'Unimplemented';
  }
}

function isNumber(exp) {
  return typeof exp === 'number';
}
```

We made a helper function called `isNumber()`. Inside the `eval()` we make a condition: if the return of the `isNumber(exp)` is true, we return `exp` itself, which is the given input. We could do that by using the `typeof` operator to check if the type of `exp` is the same as `number`. Now if we ran the same evaluation again we would have `exp` as a resolve:

``` JavaScript
const assert = require(`assert`);
const eva = new Eva();

assert.strictEqual(eva.eval(1), 1) // 1
```

The next thing `Eva` will do is evaluate a string. We can implement that by doing the same thing we just did for the numbers: implementing a helper function to do our job.

``` JavaScript
class Eva {
  eval(exp) {
    if (isNumber(exp)) {
      return exp;
    }

    if (this.isString(exp)) {
      return exp.slice(1, -1);
    }

    throw 'Unimplemented';
  }
}

function isString(exp) {
  return typeof exp === 'string' && exp[0] === '"' && exp.slice(-1) === '"';
}
```

It is important to say that `strings` in `Eva` are represented by **double quotes** `"`. The evaluated result should be the value between the quotation and everything that's in between the double quotes.

``` JavaScript
assert.strictEqual(eva.eval('"hello"'), 'hello'); // hello
```

The syntax for an addition expression on the `Eva` language is: `['+', 1, 5]`, so in order to implement the evaluation of an addition we can simply check if the first position of `exp` equals to the `+` symbol and if this condition is true, we return the sum of the second and third positions (`exp[1] and exp[2]`).

``` JavaScript
class Eva {
  eval(exp) {
    if (isNumber(exp)) {
      return exp;
    }

    if (this.isString(exp)) {
      return exp.slice(1, -1);
    }

    if (exp[0] === '+') {
      return exp[1] + exp[2];
    }

    throw 'Unimplemented';
  }
}
```

``` JavaScript
assert.strictEqual(eva.eval(['+', 1, 5]), 6); // 6
```