---
layout: post
title: Selection Sort
date: 2022-12-9
categories: Eng
tags:
  - Algorithms
---

The selection sort algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from the unsorted part and putting it at the beginning.

The algorithm maintains two subarrays in a given array. But be noted that we don't create two arrays, but operate the whole process within the original array.

- The subarray which already sorted (left part).
- The remaining subarray was unsorted (right part).

From the left most element, we itinerate the whole array one by one. In every itineration of the selection sort, the minimum element (considering ascending order) from the unsorted rigth subarray is picked and moved to the sorted subarray.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/eCcXv3avZEntkJkccU9dHA4JYR6H0jGmPdDp4COLx3W_HrP7QkYzbah4qsUmJzXXH1L2fnQ-2_Bh-OKCNuZGkXxbh3B2UbUqS-Lv5Qng46JUyM-w1LBqWKMDw6EhiiiY-JVNa8x9dg=w2400" alt="selction sort"/>

<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Illustration of Selection Sort</div>

Below is the implementation of the algorithm, we use recursion again:

```js
// swap function
const swap = (arr, a, b) => {
  const temp = arr[a];
  arr[a] = arr[b];
  arr[b] = temp;
};

// recursion realization of the selection sort
const selectRecur = (array, n) => {
  if (n === array.length) return array;

  for (let i = n; i < array.length; i++) {
    if (array[n] > array[i]) swap(array, n, i);
  }

  return selectRecur(array, n + 1);
};

// we test by a random array
const arr = [12, 10, 9, 7, 8, 5, 3, 4, 7, 7, 4, 3, 2, 1, 0, 2];
console.log(selectRecur(arr, 0));
```

<br>
