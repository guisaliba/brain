## Elixir is a dynamic and functional programming language designed to build scalable and sustainable applications. It was created by brazilian José Valim in May 2012.

It was made to be ran on Erlang's VM (BEAM). Erlang is a functional programming language, concurrent and [fail tolerant](https://stackoverflow.com/questions/3172542/are-erlang-otp-messages-reliable-can-messages-be-duplicated/3176864#3176864). Erlang offers resources to deal with concurrence, scalability and resilience, making it optimal to high-available systems that demands low latency, such as [WhatsApp](https://www.erlang-solutions.com/blog/20-years-of-open-source-erlang-openerlang-interview-with-anton-lavrik-from-whatsapp/).

One of the most known use case of a company that uses Elixir in production as one of its' main languages is **Discord**.

## What is a value?
A value is real world data. It can represent anything tangible, for example, a person's age, name, and income. When we execute values in Elixir, it returns the exact value as a result. This behavior is due to the fact that values are constant and immutable. When evaluated, they return themselves once no transformation is applied.

``` Elixir
10
```

	10

``` Elixir
Maria
```

	Maria

``` Elixir
5050.55
```

	5050.55

## Types
The fundamental types of values in Elixir are: Integer Numbers, Floating Point Numbers, Booleans, Atoms and Strings (char arrays).

## Integers
Integers are used to represent integer numerical values. You may use  __ as a separator, and you can also represent numbers in other bases such as: binary, octal and hexadecimal using prefixes **0b**, **0o** and **0x**.


``` Elixir
10
```

	10

``` Elixir
645_213_998_720
```

	645213998720

``` Elixir
0b101010
```

	42

``` Elixir
0x2A
```

	42


## Floating point numbers
Numbers that demand a decimal point after at least one digit. 64 bits precision and support "e" as exponential numbers notation.


``` Elixir
.14
```

	SyntaxError


``` Elixir
1.618
```

	1.618


``` Elixir
1.0e-10
```

	1.0e-10


## Atoms
In Elixir, an **atom** is a constant keyword which value is it's own name. You can imagine an atom as a label to represent something specific, they are a data type used to identify information in the system. Atoms always start with `:` , for example `:atom` where `atom` is the name of the atom.

``` Elixir
:atom
```

	:atom

``` Elixir
:age
```

	:age

``` Elixir
:weight
```

	:weight

## Booleans
Logical values that can either be **true** or **false**. Elixir uses two atoms to represent these values: `:true` and `:false`. These atoms are well known atoms, you don't need to put `:` before them as you should with other atoms. You can simply write `true` and `false` and it should work fine.

``` Elixir
is_atom(true)
```

	true


``` Elixir
true
```

	true


``` Elixir
false
```

	false

Another special atom related to true and false is `nil`. It represents the absence of a value, and in some occasions its' behavior is similar to `false`. Similar to `null` in JavaScript for example.

``` Elixir
nil
```

	nil

## Strings
A sequence of letters, numbers, symbols or even emojis. To represent a string in Elixir, you must begin it and end it with `""` (double quotes).

``` Elixir
"Hello, World!"
```

	"Hello, World!"

Elixir uses UTF-8 for strings, which means you can represent a large amount of characters from different languages and symbols. Elixir allows you to create strings that goes for multiple lines. To do so, you might use three double quotes at the beginning and at the end of the string: `"""`.

``` Elixir
"""
Hello, World!
This is Elixir.
It allows you to write large strings.
"""
```

	"Hello, World!\nThis is Elixir.\nIt allows you to write large strings."

## Checking for types
There are many ways to check types for a value or expression. The most common way to do so is using the function `is_` followed by the type you wanna check.

``` Elixir
is_integer(123)
```

	true


``` Elixir
is_integer(false)
```

	false


``` Elixir
is_number(1.9)
```

	false


``` Elixir
is_atom(:weight)
```

	true


``` Elixir
is_atom(true)
```

	true


``` Elixir
is_boolean(true)
```

	true


``` Elixir
is_boolean(nil)
```

	false

The function for checking **strings** is called `is_binary`.

``` Elixir
is_binary("Saliba")
```

	true


``` Elixir
is_binary(true)
```

	false


``` Elixir
is_binary("🔥")
```

	true


## Expressions
Expressions are the building blocks for logic implementation. We might build expressions to make operations for example, using operators.

``` Elixir
4 - 5
```

	-1


``` Elixir
4 / 3
```

	1.33333333333333

Even though the operands are two integer numbers, the result was a floating point number. Beside math operators, we also have logic operators that are used to make operations with booleans. These operators are: `and`, `or` and `not`.

`and`: Returns true if both operands are true. Otherwise, returns false.

``` Elixir
true and false
```

	false

`or`: Returns true if any of the operands are true. Otherwise, returns false.

``` Elixir
false or true
```

	true

`not`: Inverts the operands' value. If it is `true`, becomes `false` and vice-versa.

``` Elixir
not false
```

	true

Using a non-boolean value with these operators results in a `BadBoolean` exception.

``` Elixir
1 and false
```

	(BadBooleanError) expected a boolean on left-side of "and", got: 1

But Elixir allows you to use non-boolean values as the second argument of `and` and `or`. In case you want to use non-boolean as the first parameter, Elixir uses `&&`, `||` and `!` operators. These accept any value of any type.

In this case, only `false` and `nil` atoms will be treated as falsy values. Every other will be truthy values.

``` Elixir
1 && true
```

	true


``` Elixir
1 || true
```

	1


``` Elixir
!false
```

	true


``` Elixir
!nil
```

	true


### String concat and interpolation
Elixir uses the operator `<>` to concat two strings. String interpolation allows you to insert variables values or expressions inside of a string. In Elixir we use `#{}` for string interpolation.

``` Elixir
"UBL" <> " " <> "is cool!"
```


``` Elixir
"Where are you from? I'm from #{"Brazil"}."
```

## Variables
Variables stores values. To create one you name them, and assign a value to it. As in Elixir every expression returns something, when you call a variable, the return of it is it's value.

``` Elixir
age = 21
```

	21

Now we can use the variable `age` in other expressions:


``` Elixir
is_binary(age)
```

	false


``` Elixir
"I'm #{age} years old."
```

	"I'm 21 years old."

Every variable in Elixir is immutable. This means you cannot change a variable's value as in other programming languages, but you can reassign a value to it:

``` Elixir
age = 20
```

	20


**Variables differs from atoms in Elixir in several ways:**

1. **Value and Mutability**: Atoms are constants whose value is their own name. They are immutable and their value cannot be changed once they are defined. On the other hand, variables in Elixir are mutable and their values can be changed throughout the execution of a program.
2. **Syntax and Naming**: Atoms in Elixir are always prefixed with a colon `:` and can contain any Unicode character. They are typically used to identify specific states or conditions in a program. Variables, on the other hand, do not have a colon prefix and must start with an underscore or a Unicode letter that is not in uppercase or titlecase. The variable name can continue with a sequence of Unicode letters, numbers, and underscores.
3. **Usage**: Atoms are commonly used as keys in maps, as they are more efficient than strings for this purpose. Variables, on the other hand, are used to store and manipulate data in a program.


## Pattern Matching
When declaring a variable, we use the pattern matching operator `=`. This way you can create a variable and assign a value to it. Although the symbol for doing this matching is `=`, the left and right side of a pattern matching have different "weights".

``` Elixir
name = "Saliba"
```

Assigning the value `Saliba` to the variable `name` is only possible because the variable is at the left side of the pattern matching. If it were to be at the right side, this wouldn't work. 

This means that in Elixir, the left side of a pattern matching has more "power" than the right side.

``` Elixir
"Saliba" = name
```

	error: undefined variable "name"

But once a value has been assigned to a variable, it is possible to use it at the right side, just like the example below:

``` Elixir
20 = age
```

	20

An important reminder: pattern matching isn't just simply value attribution to a variable.

## Lists
Collections are data structures that contains zero or more values. The most used type of collection in Elixir are **lists**. A list can be empty or contain one or more elements.

``` Elixir
# Empty List
[]
```

	[]


``` Elixir
[1]
```

	[1]

``` Elixir
[3, 45, 78, 21]
```

	[3, 45, 78, 21]

Lists start with `[` and end with `]`. Values in a list are separated by comma `,`. You might have a list with values of different types as well:

``` Elixir
[1, "House", :age, true]
```

	[1, "House", :age, true]

And also a list that contains another list:

``` Elixir
[1, [1, 2], 3]
```

	[1, [1, 2], 3]

This is how pattern matching works with lists:

``` Elixir
[head | tail] = [1, 2, 3]
```

	[1, 2, 3]

``` Elixir
head
```

	1


``` Elixir
tail
```

	[2, 3]

The `head` variable represents the first element of the list, and `tail` represents the remaining elements of the list. Since this list have three elements but only two variables being assigned to it, `head` will represent the first element and `tail` the remaining two values. 

Another example:

``` Elixir
[first, second | rest] = [45, 67, 784, 3500]
```

	[45, 67, 784, 3500]


``` Elixir
first
```

	45


``` Elixir
second
```

	67


``` Elixir
rest
```

	[784, 3500]

At the end of a list there is always an empty list.

In pattern matching, you can use the operator `_` to ignore something. See the example below:

``` Elixir
[head | __] = [500, 250, 125]
```


``` Elixir
head
```

	500


``` Elixir
__
```

	Nothing is attributed to _ .

Lists in Elixir grows from the head which means that in order to add a new element to a list, we might put it in the left-most position of the list. We can use the operator `|` to do so:

``` Elixir
[1 | [3, 4]]
```

	[1, 3, 4]


``` Elixir
[2, 3, 4 | [5, 6, 7]]
```

	[2, 3, 4, 5 , 6, 7]

It is also possible to make operations with lists, such as subtracting two lists, using the operand `--/2`. This operand is in fact a function, its name is `--` and it accepts `2` arguments:

``` Elixir
[1, 2, 3] -- [1, 3]
```

	[2]


## Tuples
A tuple is an ordered collection of elements. Tuples are defined using `{}` and its values are separated by comma `,`.

``` Elixir
# Empty Tuple
{}
```

	{}

``` Elixir
{:name, "Saliba", :age, 21}
```

	{:name, "Saliba", :age, 21}

Pattern matching with tuples are as simple as:

``` Elixir
person = {:name, "Saliba", :age, 21}
```

	{:name, "Saliba", :age, 21}

To retrieve specific elements of a tuple, you could match them as:

``` Elixir
{:name, name, _, _} = person
```

	{:name, "Saliba", :age, 21}

Now the variable name represents the element `"Saliba"` of the tuple.

``` Elixir
name
```

	"Saliba"


## Maps
