# subject: [[trivias]]
# topics: #clean-code #interesting
---
_I don't even know if what I'm about to write is indeed some kind of truth. I accidentally came across this excerpt of a [book at O'Reilly](https://learning.oreilly.com/library/view/your-code-as/9781680500813/f_0041.html) website while researching on "Negative Space Programming"._

All programming languages use whitespaces as indentation, some even treats it as a requirement (e.g.: Python) for the compiler/interpreter to actually build your code. But in most cases, and even for those that treats it as something more meaningful, indentation is more about the code's shape, readability and organization.

The idea of indentation as something else than just the shape of the code is backed up by [research](https://learning.oreilly.com/library/view/your-code-as/9781680500813/f_0105.html#d2148e1073)where it is actually treated as a **proxy for complexity**. It is a simple metric, fast, and language-independent, because the concept of indentation applies to any programming language, be it Java, Python, Closure or C.

This idea states that we can measure the complexity of a program by counting how many times logical indentations appears in the code. Logical indentation is defined here as either **four spaces** or **one tab** while empty and blank lines are ignored. Calculating those is trivial: just read a file line by line and count the number of times a logical indentation appeared.

If I did have a script to calculate logical indentations for a file, then I could calculate the average of logical indentations in that file, by dividing the total numbers of line by the occurrences for a logical indentation. The higher the average, the more complex the program would appear to be.

And why is that? Because it essentially means that if my code has a lot of indenting, it probably has a lot of nested conditions. There, that's the complexity measurement of the program by looking at it's indentation only.

Of course analyzing indentation alone is not supposed to produce absolute truths, but when you do find excess complexity, you have a clear candidate for refactoring.