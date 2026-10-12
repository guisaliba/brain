An array is a simple contiguous memory space, ranging from 0 to N that stores data. In other words arrays are fixed size, contiguous memory chunks. It is a common data structure.

This means you cannot grow it. You cannot simply create an array `int[3]` that is supposed to store three integers and then all of a sudden create a fourth position (`arr[3]`) to store a new element.

``` js
// This is something like an array, it is a contiguous space of memory.

const a = new ArrayBuffer(6);
console.log(a);

// This is a view of the array buffer, it is a way to access the array buffer. Each value is 8 bits.

const a8 = new Uint8Array(a);
a8[0] = 45;
a8[2] = 0x45;

console.log(a); // ArrayBuffer { [Uint8Contents]: <2d 00 45 00 00 00>, byteLength: 6 }
  
// The offset of this view is (position * 8 bits). So when we set the value of the second position to 0x45, it is actually setting the third byte of the array buffer (because each byte is 8 bits).

// Another view but each value is 16 bits.
const a16 = new Uint16Array(a);
a16[2] = 0x4545;

console.log(a); // ArrayBuffer { [Uint8Contents]: <2d 00 45 00 45 45>, byteLength: 6 }

// But here the offset is (position * 16 bits). So when we set the value of the second position to 0x4545, it is actually setting the third and fourth bytes of the array buffer (because each byte is 8 bits).
```

In arrays there are no insertion, push or pop and not even deletion. All you're doing is setting a value for a position.

If you're inserting an element into an array at `index = 2` let's say, you're not putting it in there, you're just setting the value of that index to be your element. The same happens for deletion.

If you delete the element at index[2] you're not removing it from there you're just setting it's value to something that is actually nothing (`null` in JavaScript for example but you can think of it as zero or nothing as well).

Doesn't mean you cannot write these insert and deletion methods though, that is totally possible, more recent languages actually do have these methods already implemented.