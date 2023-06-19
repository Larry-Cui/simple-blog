---
layout: post
title: Quicksort
date: 2022-09-01
categories: Eng
tags:
  - Algorithms
---

## History

According to [wikipedia](https://en.wikipedia.org/wiki/Quicksort), quicksort is an in-place sorting algorithm. Developed by British computer scientist Tony Hoare in 1959 and published in 1961, it is still a commonly used algorithm for sorting.

## Algorithm explained

Quicksort is a divide-and-conquer algorithm. It works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. For this reason, it is sometimes called partition-exchange sort The sub-arrays are then sorted recursively. Because of its nature of algorithm, recurisve code is best suited for quicksort.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/ohci3ypZ6NCilVOE3CHFCJfNbMU1U7GbxExrnhuzeZRaAsx5BQmfk7kg_ExAoqa0YLdvEwRK0-o9Az34dNrg8Sa01gHKTAu-zKuBuQuLf-uz36sbU_xjb3CffZE7o0841C3TQzXnGQ=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Illustration of Quicksort</div>

<br>

Quicksort is a comparison sort, meaning that it can sort items of any type for which a "less-than" relation (formally, a total order) is defined. Efficient implementations of Quicksort are not a stable sort, meaning that the relative order of equal sort items is not preserved.

## Code example

Here's the code in JavaScript for quicksort:

```js
/* ************************* */
// Quicksort recursion code
/* ************************* */

function quicksort(array) {
	if (array.length <= 1) {
		return array;
	}

	// we pick the first element of
	// array or sub-array as the pivot
	const pivot = array[0];

	// we create two sub-arrays to store elements
	// [] = new Array()
	let left = [];
	let right = [];

	// first element has been picked as pivot
	// so we start from index 1
	for (let i = 1; i < array.length; i++) {
		array[i] < pivot ? left.push(array[i]) : right.push(array[i]);
	}

	// recursion happens here
	// unlike others, it's a binary recursion
	const partition_left_sort = quicksort(left);
	const partition_right_sort = quicksort(right);

	// The concat() method is used to merge two or more arrays.
	// This method does not change the existing arrays,
	// but instead returns a new array.
	return partition_left_sort.concat(pivot, partition_right_sort);
}
```

Some notes to take here:

- before every fork to dig into the recursion, the array/sub-array has been separated as two sub-arrays less than and greater than the pivot.
- when roll back from the single element array, `concat` is the key to stitch them together, and that's how we can get a sorted array back on the top. No comparison is needed at the `concat` steps.
- we can pick the pivot element by any rules. The first, the last, the middle, or even a random one, the results are the same.

## Time complexity

At the first fork, which means we pick the pivot, and partition the array into two sub-arrays, we need $n-1$ comparison and pushes.

At the second fork, we pick two pivots and carry out $n-3$ times of comparison and pushes, and go on at the same manner for further forks.

If we are lucky to pick all pivots that can result in two same size sub-arrays, we will have $\log_2 n$ forks in total, so the complexity is $O (n \log n)$. If we are not such luck, we might end up with sub-arrays of $n/3$ and $2n/3$ sizes. In that case, we will have $\log_3 n$ forks, but the complexity is still $O (n \log n)$.

Imagine however, we pick the smallest or largest element of the arrays each time before the fork, we end up with $n$ forks before we get the single element array at the uttermost level of the bichotomy. The total comparison and pushes is:

$$
(n-1)+(n-2)+(n-3)+ \dots + 1 = \frac{n\times(n-1)}{2}
$$

So in worst scenario, the time complexity of quicksort is $O(n^2)$.

We won't be so unluck, as for a random array, the probability of selecting the smallest or greatest number each time is close to zero. However, if we are given an already sorted array, for example, in an ascending order, and we pick the first element as pivot every time, we will step into the worst scenario without doubt!

A clever way to mitigate this risk is to pick the pivot randomly. In coding practice, we usually stick to the first or last element as pivot for easy coding, but choose a random element and swap it with the first/last element beforehand.

<br>
