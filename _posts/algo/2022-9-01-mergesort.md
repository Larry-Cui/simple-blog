---
layout: post
title: Mergesort
date: 2022-09-01
categories: Eng
tags:
  - Algorithms
---

## History

According to [wikipedia](https://en.wikipedia.org/wiki/Merge_sort), merge sort (also commonly spelled as mergesort) is an efficient, general-purpose, and comparison-based sorting algorithm. Most implementations produce a stable sort, which means that the order of equal elements is the same in the input and output. Merge sort is a divide-and-conquer algorithm that was invented by John von Neumann in 1945.

## Algorithm explained

In quicksort, divide and compare happen before the fork. When the recursion goes down to the end, we only need to stitch individual elements back together. In mergesort, however, an array of elements is always divided equally without comparing. when the recursion goes down to the end, compare happens and stitch back with the designated order, ascending or descending.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/EIbh-aP55dd4uCU2fMlWrBc2IkVW31HUUh0pGZfdtt2CAk7HI66xSOirdAI6BZz5tO-LWFEqCIduZeeIoLvIt7NOpBosgZ1hwra7u12_MMmuLWPjqMsuEhDzlYrx-2Cu1jk4fER_-g=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Illustration of Mergesort</div>

<br>

## Code example

Here's the code in JavaScript for mergesort:

```js
/* ************************* */
// Mergesort recursion code
/* ************************* */

function mergeSort(array) {
	const length = array.length;

	// roll back condition:
	// if a sub-array's length is equal to or less than 1,
	// we are at the leaves of the binary tree.
	if (length <= 1) return array;

	// partitioning of the array/sub-array
	// the array/sub-array haven't been sorted yet
	const mid = Math.floor(length / 2);
	const sortedLeftArray = mergeSort(array.slice(0, mid));
	const sortedRightArray = mergeSort(array.slice(mid));

	// here below is the sorting and merging process
	// when the recursion reach the end of leaves and roll back
	// the program will continue as below

	// we define a merge function first
	function merge(sortedLeftArray, sortedRightArray) {
		let result = [];

		// by combining push() and shift(), elements
		// in left and right arrays are extracted and pushed to result

		while (sortedLeftArray.length && sortedRightArray.length) {
			// when array lenght = 0, bolean value would be false!!!

			if (sortedLeftArray[0] < sortedRightArray[0]) {
				result.push(sortedLeftArray.shift());
			} else {
				result.push(sortedRightArray.shift());
			}
		}

		/* Either left/right array will be empty or both */
		return [...result, ...sortedLeftArray, ...sortedRightArray];
	}

	// we call the merge function //
	// merge() function constructs sorted array/sub-array,
	// but it needs to be returned to
	// above place where the mergeSort() is called to be
	// further compared and merged.
	return merge(sortedLeftArray, sortedRightArray);
}
```

Some notes to take here:

- before every fork, the array/sub-array has been divided equally into two sub-arrays without sorting, so the structure of the recursion is always a binary tree.
- when roll back from the leaves, `merge()` is working to compare(sort) and combine sub-arrays.
- the height of the binary tree is always $\log n$.

## Time complexity

The dividing part of the mergesort involves no comparison, so we can simply ignore it.

For the sorting and merging part from bottom up, we have $n/2$ comparing and sorting for each level. With a total of $\log n$ levels (height), the complexity is $n \log n$.

<br>
