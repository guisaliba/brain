# what are pointers?
pointers are literally what they say they are: pointers to something. but wait, what does that mean?
it means that a pointer (or any pointer) exists to point to something known. "something known" is actually a memory address that stores some value.
if a memory address stores a value, then we could get (or reference) this value by pointing to it, instead of accessing it and kind of copying the value being held on that address.
this is called as "reference passing" which is, passing the value from a memory address to another address by referencing it. we can visualize this in C e.g.:
``` C
const int x = 10;
const int *y = &x;
```
what happens here is that "x", a variable that is the representation of a memory address, holds the integer value of 10. then, the variable "y" points to whatever "x" is holding.
this happens not by pointing to whatever value "x" is holding but to the address of "x".

in other words, if "x" lives in a memory address `0xCCCC` (hexadecimal representation) and stores the int value `10`, then "y" could live in another address `0xCCD0` and store `0xCCCC`, which is the address of "x", not the value `10`.
in the end, accessing the value at `*y` will return us `10`, but it is not **holding** `10`, instead it holds whatever currently lives at the memory address of "x".