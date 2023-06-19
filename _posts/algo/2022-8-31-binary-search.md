---
layout: post
title: Binary Search
date: 2022-08-31
categories: Eng
tags:
  - Algorithms
---

<p style="color: MediumVioletRed"> **Comment:** I made the post date at Sept. 01, 2022 at first. It cost me the whole morning trying to make this post show up on the blog but failed. It turns out that you cannot pre-date post, otherwise it cannot be rendered by github. An 3-hour expensive lesson!~</p>

If you are given an array of un-ordered numbers, and asked to find if there's a number, let's say, "23", in that array. How can you do the search?

Of course, we can pick the number one by one from the array, and compare it with number 23, if it's a match, we find the answer; if there's no match after we go down through the whole array, we conclude number 23 is not in the array.

Here is the code of the above algorithm:

```js
// "return" will stop execution of the program
// but we cannot use retun outside of a function
const logFound = (i) => {
	return "found 23 at index: " + i;
};

// loop to find "23"
for (let i = 0; i < arr.length; i++) {
	if (arr[i] === 23) logFound(i);
}

// if not found, we come here to output "not found"
console.log("23 not found!");
```

This is called linear search, since we search the target from the array one by one from first to last, in a linear way. If, However, you are asked to find another number, linear search means you have to run from the beginning again. When we need to search for infinite times, and the array is huge, linear search is too expensive. This is when binary search kicks in.

Binary Search only works on ordered list of numbers. The idea of the algorithm is that we pick the center index of the array and compare it with the target number we want to match. If not found, we know if the target is greater or less than the center index number, then we can go for the first or second part of the array to repeat the binary search. You can easily tell that one round of pick and compare will cut the "suspects" in half, which is how the search name comes from.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/ecpWDWiBSUkJ2A5DjEl3uj9JSn8swluTP-T4kovyzKZLQ5CQGl0gXXQb7Tf2hNMgndkcxIf3ZEz048F1V3XvNHD2T35Hn4sjyjdD8utBVG3UYjtwRzZFSaVF68RbWkvAFeVm9aHI5g=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Binary Search Illustration</div>

<br>

Here is the code for binary search in Javascript:

```js
// return a Boolean: true if x is in the array, and false otherwise
function binarySearch(array, x) {
	let L = 0;
	let R = array.length - 1;
	let midPoint;

	// we assume the array has been sorted in an ascending order.
	// if not, we need to sort the array first.

	// check if x is within the scope of the array.
	if (x < array[0] || x > array[R]) return false;

	// while loop + L/R modification
	while (L <= R) {
		midPoint = Math.floor((L + R) / 2);
		if (x === array[midPoint])
			return `true, number ${x} is at array[${midPoint}].`;
		else if (x > array[midPoint]) L = midPoint + 1;
		else if (x < array[midPoint]) R = midPoint - 1;
	}

	return `false, number ${x} is not in the array!`;
}
```

<br>
