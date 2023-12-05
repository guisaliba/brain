# Big O is a way to categorize your algorithm on time and memory complexity based on the input. It tells how your algorithm reacts to different given inputs.

## Growth is with respect to the input
As your input grows, how fast does computation or memory grow? The growth of these two are **directly** related to the input, if the input grows, they will grow as well.

Take a look at this example:
``` typescript
function sum_char_codes(n: string): number {
	let sum = 0;
	for (let i = 0; i < n.length; i++) {
		sum += n.charCodeAt(i);
	}

	return sum;
}
```

If you analyze it you will realize that the function iterates through every element (char) of a given string and for every iteration, it takes the char code on that position and adds its value to sum. What does it mean? It means that for every additional char on the string, there is an additional operation for the algorithm to do: add the char code to the sum.

**That is O(n)**. But how can you tell that? The simplest trick is to simply look for loops. If you see a loop through the input (in this case, a string a.k.a an array of chars) it means that you are doing operations based on the length of the input. Your algorithm grows with the input's length: **O(n)**.

Let's take a look at another example:

``` typescript
function sum_char_codes(n: string): number {
	let sum = 0;
	for (let i = 0; i < n.length; i++) {
		sum += n.charCodeAt(i);
	}

	// capital E
	if (n.charCodeAt(i) === 69) {
		return sum;
	}

	return sum;
}
```

This is the same example as before but now we're putting a conditional that says "if you run into a capital E character on the string, returns immediately the value of sum". What would be the running time for this algorithm? It would still be **O(n)**.

Why is it still O(n), does it mean that the conditional change nothing? Yes, it changes nothing. And that's due to in order to determine the running time of an algorithm, we always consider the worst case scenario.

Let's say the capital E is at the last position of the input. If that is the case, the algorithm would have to iterate through the entire input before returning something meaning that if you add an element to the input, there will be an extra iteration. 
 
Ok so what if the capital E is at the middle of the input or even better, at the third last position of the input? Well then that would be a O(n / 2) or an O(n - 3) which is in other words, an O(n).

Why? Because you **drop constants**. Speculating that kind of scenario with a "what if?" question means that you're no longer thinking about the worst case scenario, and that breaks the set of rules that determines the Big O for an algorithm. **Always consider worst case.** Worst case is the way you measure how your algorithm reacts to the input's growth.

## Common complexities
- **O(1)**, **constant time**. No matter how big the input is, it does the same amount of operations every single time. That's (almost) perfection for an algorithm's running time.
- **O(log n)**, it grows linear. In other words, it is pretty fast and that's a based 2 logarithm btw.
- **O(n log n)**, which is pretty ok, not the best but good.
- **O(n ^ 2)**, this grows pretty fast and a large input here means that the running time for this will be insanely huge as well. One of the worst scenarios.
- **O(2 ^n) and O(n!)**, these are so huge that they cannot run on traditional computers. These could take thousands and thousand of years of running time. That's it.

``` typescript
function sum_char_codes(n: string): number {
	let sum = 0;
	for (let i = 0; i < n.length; i++) {
		for (let j = 0; j < n.length; j++) {
			sum += n.charCodeAt(i)
		}
	}

	return sum;
}
```

You can easily tell that the running time for this algorithm is **O(n^2)**. Remember the trick to look at the loops? That's how you can tell. There are two loops in this one and they are nested which means that for every iteration on **i** we iterate again. You can imagine these as graphs: for every vertical line on the graph, we look at an horizontal line on the graph.

Short story short, these are the three main concepts to keep in mind when talking about Big O:

1. Growth is related to input;
2. Constants are dropped;
3. Worst case scenario is the way to measure.