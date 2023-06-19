---
layout: post
title: Insertion Sort
date: 2022-08-30
categories: Eng
tags:
  - Algorithms
---

Insertion sort is among the first models we learn about algorithms. It sorts an array of numbers from left to right, make comparison with all sorted numbers to the left, and act on one move when it finds its place in the left sub-array: inserting into the right place.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh4.googleusercontent.com/IOEXfpxbHbHvOha4qOjBAmFw8YDm-7rWsENDsdvpXOjsFq7GToDlgTXS3ikMXYsPNl0=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Insertion Sort Illustration</div>
<br>

We implement insertion sort with Javascript:

```js
// Let "array" be an unsorted array of numbers

// This implements the shift function
function shift(array, index1, index2) {
	if (index1 === index2) return array;
	// This happens when the element is greater or equal to the number right to its left

	const temp = array[index1];
	for (let i = index1; i > index2; i--) {
		array[i] = array[i - 1];
		// move all numbers at and above index2 one place right-ward
	}
	array[index2] = temp;
	// move number at index1 to index2, finish shift

	return array;
}

// You cannot really make an instant shift of array or part of array.
// As inserting one person into the people at the table,
// everyone has to move one chair forward to make one seat for the inserting guy.

//INSERT SORT
function insertionSort(array) {
	for (let i = 1; i < array.length; i++) {
		let j = i - 1;

		for (j; j >= 0; j--) {
			if (array[i] >= array[j]) break;
			// break means we don't need to compare furhter
		}

		shift(array, i, j + 1);
	}

	return array;
}
```

<br>
