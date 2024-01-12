Keeping data in sorted order is a daily task we perform without even knowing. Let's say you have a lot of books in your shelf and you would like to organize them by their numbers of pages in a crescent way. You could use an algorithm to do that.

Formally saying, **sorting is arranging the elements in a list or collection in increasing or decreasing order of some property**. In the example above, the books (elements) were sorted in the shelf (collection) in increasing order by the number of pages (property). To sort a list or a collection, **all of its elements should be of the same data type**, usually we sort lists or collections of integers.

Sorting data is extremely helpful for computational processes. If the books on the shelf were not sorted, to retrieve a book we would have to go through all of them until we find the desired book.

In other words, if there are **n elements in the list**, we would make **n comparisons** in the worst case meaning that we had to look for every element in the list until we found our element, because it was the last element in the list. This is called **linear search**.

If elements were sorted, we could use algorithms like a **binary search** which would only cost `log n` comparisons, a number insanely smaller than the linear search's cost.

Some of the most famous sorting algorithms are:

- Bubble Sort
- Selection Sort
- Insertion Sort
- Merge Sort
- Quick Sort
- Heap Sort
- Counting Sort
- Radix Sort

There are many ways to classify a sorting algorithms: **1. Time complexity 2. Space complexity (memory usage) 3. Stability 4. Internal Sort vs External Sort 5. Recursive or Non-recursive**

1. Time complexity is how much time the algorithm takes to sort elements in respect to the input's size.
2. Some sorting algorithms use constant amounts of memory to rearrange the elements in the list, but some, like Merge Sort uses extra memory to temporarily store data.
3. A stable sorting algorithm guarantees that in the case of equality of key, it preserves the relative (original) order of elements.
4. When all records that need to be sorted are in main memory or RAM, it is an internal sort. When records are on disk/tapes it is an external sort.
5. Some sorting algorithms like Quick or Merge Sort are recursive, while others like Insertion and Selection sort are not recursive.