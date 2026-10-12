A selection sort algorithm takes an array of size "n" and iterates through it. For each iteration, it finds the smallest element in the array and swaps it with the element at the current index. The **time complexity** of this algorithm is **O(n^2)** and the **space complexity** is **O(1)**.

For now, we can definitely visualize that there will be two loops in this algorithm.  

The first loop would iterate through every element in the array and the second would find the smallest element in the array. The second loop appears nested inside the first loop, casing the time complexity for this algorithm to be O(n^2).

The first loop iterates through every element in the array until the last position of the array. That's because when the loop gets to the last element in the array (n - 1), the last element should already be the greatest element in the array, a consequence of every iteration that came before which already ordered the array.

The second loop iterates through every element from the minimum index (i+1) to the end of the array. And that is because the second loop checks if there is another element in the array smaller than the current minimum index, so it compares every element from the current minimum beyond.  

That's why space complexity for the selection sort algorithm is **O(1)**.

```js
// A = array of size n
// n = size of array
// i = current index
// j = index of the smallest element in the array

for (let i = 0; i < n - 1; i++) {
    let minI = i;

    for (j = i + 1; j < n; j++) {
      if (A[j] < A[minI]) {
        // Sets "j" index as the current minimum index, so the algorithm
        // only iterates from the current minimum and further.
        minI = j;
      }
    }

    let temp = A[i];
    A[i] = A[minI];
    A[minI] = temp;
  }
```