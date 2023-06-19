---
layout: post
title: Bubble Sort
date: 2022-08-30
categories: Eng
tags:
  - Algorithms
---

Bubble sort is always discussed along side insertion sort. Contrary to sorting from left to right by insertion sort, Bubble sort works from right (last) to left (first). Furthermore, Bubble sort uses swap rather than shift to order numbers. It's working as a compare and swap model.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/4Pu3g3Sv_ou0xWLc1ywBP4mrQnuDXk0Vwg2zuDyYwMDcDKo-RO6Wrfr3CED5JNd3tsYk3eUdv6yxq41zzIoqjNYHqWhnsEFi5B1d2nSifjxH_doZ5vqK2bPBm7m-ofJ1vZ7utSHB0A=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Bubble Sort Illustration</div>
<br>

We implement bubble sort with Javascript, it's in fact more straight forward than insertion sort:

```js
// Let "array" be an unsorted array of numbers

// This implements the swap function
// Unlike shift function, swap deals with two indices/numbers only
function swap(array, index1, index2) {
	const temp = array[index2];
	array[index2] = array[index1];
	array[index1] = temp;
	return array;
}

// BUBBLE SORT
function bubbleSort(array) {
	for (let i = 0; i <= array.length - 2; i++) {
		// for n numbers, we only need to compare and swap at most (n-1) times

		for (let j = 0; j <= array.length - 2 - i; j++) {
			// after each loop of comparison and swap,
			//the right most ordered elements plus one
			if (array[j + 1] < array[j]) {
				swap(array, j, j + 1);
			}
		}
	}
	return array;
}
```

In fact, the above algorithm can be optimized: think if in any loop of compare and swap, if no swap happens, what does it mean? It means the array has already been sorted!

The updated bubbleSort function is like this:

```js
// BUBBLE SORT
function bubbleSort(array) {
	for (let i = 0; i <= array.length - 2; i++) {
		// for n numbers, we only need to compare and swap at most (n-1) times

		let counter = 0;
		// add a counter

		for (let j = 0; j <= array.length - 2 - i; j++) {
			// after each loop of comparison and swap,
			// the right most ordered elements plus one

			if (array[j + 1] < array[j]) {
				swap(array, j, j + 1);
				counter = counter + 1;
			}
		}

		if (counter === 0) break;
		// when in one loop counter ends up at 0,
		// we break the whole loop and give the array directly!
	}
	return array;
}
```

<br>
