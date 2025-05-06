# what are pointers?
pointers are literally what they say they are: pointers to something. but wait, what does that mean?

it means that a pointer (or any pointer) exists to point at something known. "something known" is actually a memory address that stores some value.

if a memory address stores a value, then we could get (or reference) this value by pointing to it, instead of accessing it and kind of copying the value being held on that address.

this means that we can access (and even modify) the value living in an address without actually having to access that address directly.

we can visualize this in C e.g.:
``` C
int x = 10; // x is a variable storing the value 10
int *y = &x; // y is a pointer storing the address of x
printf("%d", *y); // 10

*y = 20;
printf("%d", x); // 20
```
what happens here is that "x", a named location that has a memory address, holds the integer value of 10. then, the variable "y" points to whatever "x" is holding.
this happens not by pointing to whatever value "x" is holding but to the address of "x".

in other words, if "x" lives in a memory address `0xCCCC` (hexadecimal representation) and stores the int value `10`, then "y" could live in another address `0xCCD0` and store `0xCCCC`, which is the address of "x", not the value `10`.

in the end, accessing the value at `*y` will return us `10`, but variable `y` is **not holding** `10`, instead it is holding whatever currently lives at the memory address of "x".

we can change what lives at `0xCCCC` through the `*y` pointer, not having to directly access that address in order to modify what it holds.

if we were to do something like `*y = 20` and then access `x` again, we would have `20` instead of the original value `10`. this happened without us accessing `x` directly.

## a better visualization
### memory state after variable declaration

| Variable Name | Memory Address | Value Stored       | Description                      |
| ------------- | -------------- | ------------------ | -------------------------------- |
| `x`           | `0xAF28`       | `10` (integer)     | Integer variable storing 10      |
| `y`           | `0xBF44`       | `0xAF28` (address) | Pointer storing the address of x |

### memory state after let's say `*y = 84`

| Variable Name | Memory Address | Value Stored       | Description                      |
| ------------- | -------------- | ------------------ | -------------------------------- |
| `x`           | `0xAF28`       | `84` (integer)     | Value changed via pointer        |
| `y`           | `0xBF44`       | `0xAF28` (address) | Pointer still stores x's address |
