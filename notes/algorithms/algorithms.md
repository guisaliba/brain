---
title: What are algorithms?
description: An introduction to algorithms and their role in computing.
tags:
  - algorithms
  - cs
---
Algorithms are a set of instructions or rules that are followed to perform a task or solve a problem. They are fundamental to computing, as they enable computers to perform complex operations efficiently.

Algorithms are used in computing to perform specific tasks, such as searching and sorting data. They are also used to help execute the necessary instructions to run a program.

In computing, an algorithm is a sequence of steps to be taken from an **Input** to obtain an **Output**. We define **Input** as **ENTRY** and **Output** as **EXIT**.

But this does not mean that for each Input there is only one algorithm that leads to an Output. Nor does it mean that there is only one Output for each Input.

Algorithms are developed for any type of problem, and their function is to solve the problem for which they were developed, even if this problem may vary numerous times.

In summary:

- An algorithm is a function, which given an **Input** points to an **Output**. We can only hope that this Output is a correct answer to the problem.
- To prove that the output is indeed a correct answer to the problem, we most likely use loops, recursions, and conditions. We call this **Proof by Induction**.
- Algorithms must always be efficient and we measure the efficiency of an algorithm not by the time it takes to be executed but rather by the number of operations it needs to perform in order to solve it's problem.

An example of an algorithm capable of solving a problem is the **binary search algorithm**, it is used to locate a specific element in a set of organized data. This algorithm works by dividing a list (or any other set of organized data) in half, comparing the middle element with the target element, and then deciding whether the target element is in the first or second set of data.

This process is repeated until the target element is found. A representation of this algorithm in JavaScript could be written like the example below:

``` js
function binarySearch(array, target) {
	let left = 0;
	let right = array.length - 1;
	while (left <= right) {
		let middle = Math.floor((left + right) / 2);
		let value = array[middle];
		if (value === target) {
				return middle;
			} else if (value < target) {
					left = middle + 1;
				} else {
					right = middle - 1;
				}
			}	
			return -1;
		}
```

The `binarySearch` JavaScript function is a representation of the **binary search algorithm**.

The variables `left` and `right` are used to define the search range limits. `left` starts at **0** because it is the first position of the array, `index 0`, commonly called the starting position. The `right` variable is defined as the last index of the array, i.e. `array.length - 1`, because the index starts at 0. As the index of the array starts at 0, the last index of it is `array.length - 1`.

In an array of 6 numbers (1 to 6), for example, the first index would be 0, which would have as its corresponding value the number 1. The last index would be 5, which would have as its value the number 6.

The `while` loop is used to traverse the interval until the target element is found or until there are no more elements to be checked.

The `middle` is used to define the position of the middle of the interval.

The variable `value` is used to store the value of the current position of the interval.

If the value is equal to the target element, the algorithm returns the index of the target element. If the value is less than the target element, the algorithm moves to the next half of the interval.

If the value is greater than the target element, the algorithm moves back to the previous half of the interval. If the element is not found, the algorithm returns -1.