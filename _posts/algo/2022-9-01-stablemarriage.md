---
layout: post
title: Stable Marriage Problem
date: 2022-09-01
categories: Eng
tags:
  - Algorithms
---

Table of Contents:

- [Introduction](#introduction)
- [Algorithm explained](#algorithm-explained)
	- [Pseudocode](#pseudocode)
- [Code example](#code-example)
	- [The variables we need:](#the-variables-we-need)
	- [helper functions](#helper-functions)
	- [Key function to execute the algorithm](#key-function-to-execute-the-algorithm)
	- [Final kick](#final-kick)
	- [An test result](#an-test-result)
- [Proof of the algorithm](#proof-of-the-algorithm)
- [Time complexity](#time-complexity)

## Introduction

According to [wikipedia](https://en.wikipedia.org/wiki/Stable_marriage_problem), the stable marriage problem (also stable matching problem or SMP) is the problem of finding a stable matching between two equally sized sets of elements given an ordering of preferences for each element.

The stable marriage problem has been stated as follows:

> Given n men and n women, where each person has ranked all members of the opposite sex in order of preference, marry the men and women together such that there are no two people of opposite sex who would both rather have each other than their current partners. When there are no such pairs of people, the set of marriages is deemed stable.

A matching is not stable if:

> When given a married pair, X-a and Y-b, if man X prefers b more than his current wife a and woman b prefers X more than her current man Y, then X-b is called a dissatised pair. X-b also has a very confusing name, the unstable pair, although they seem more stale than the currently matched pairs.

In other words, a matching is stable when there does not exist any pair which both prefer each other to their current partner under the matching.

## Algorithm explained

In 1962, David Gale and Lloyd Shapley proved that, for any equal number of men and women, it is always possible to solve the SMP and make all marriages stable.

The Gale–Shapley algorithm (also known as the deferred acceptance algorithm) can be summarized as follows:

- Use the marriage as an example. We assume it's men that alwarys make the proposal, women can accept or reject it, but never propose back to men.
- each unengaged man proposes to the woman he prefers most (the one comes first on his waiting list), and at the same time delete this women from his waiting list.
- If the woman being proposed is unmatched, she accepts the proposal from the man. If the woman is already engaged, she checks her waiting list (no entry of the woman's waiting list will be deleted or changed, it keeps whole throughout the matching process): if the proposer comes after the man she already engaged, she turns down the proposal; if comes before, she drops the current man and accept the latter's offer.
- repeat above steps until all men and women are matched.

### Pseudocode

<div style="display: flex; justify-content: center">
<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/BnOkDtVASEAaZhbMfItoj1k17O9GJc2HZJLDvMEksEc1CHqeoKXaabFYhKvb8-37be3YZMEFGnZ-5Grild8npjp97vHntzxsxADhKWvGj-JUPhb3NVGUxT1mR2_P4e3u1XiOqTwItA=w2400" alt="insertion sort"/></div>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Pseudocode for Stable Marriage Algorithm</div>

<br>

## Code example

The code in JavaScript for this algorithm is a bit lengthy, we need to divide it into several parts and elaborate one by one.

### The variables we need:

- `Num` is the number of men/women
- we use array to store men/women info. Each man/woman takes an entry of the array, and in each entry, as you will see below, store his/her waiting(wishing) list for the other half
- we also have a counter to check how many loops we use to get the final result

```js
const Num = 5;
const Men = new Array(Num);
const Women = new Array(Num);

// set a counter to see how many loops we need
// to match all pairs
let counter = 1;
```

### helper functions

- `swap` is a common function to swap elements in an array
- `arrFill` is to fill the array from 1 - `num`
- `arrScramble` as its name suggests, to scramble the array elements
- `arrGen` is to finish the final work. Notice we set the index 0 element of each entry to false

```js
const swap = (arr, i, j) => {
	const box = arr[i];
	arr[i] = arr[j];
	arr[j] = box;
};

// we first fill an array sequentially
const arrFill = (arr) => {
	for (let i = 0; i < arr.length - 1; i++) {
		arr[i + 1] = i;
	}
};

// we scramble the elements in an array
const arrScramble = (arr) => {
	for (let i = 1; i < arr.length - 1; i++) {
		const randomIndex = Math.ceil(Math.random() * (arr.length - 1));
		swap(arr, 1, randomIndex);
	}
};

// we create waiting list for both men and women
const arrGen = (arr) => {
	for (let i = 0; i < arr.length; i++) {
		arr[i] = new Array(arr.length + 1);
		arr[i][0] = false;

		arrFill(arr[i]);
		arrScramble(arr[i]);
	}

	return arr;
};
```

### Key function to execute the algorithm

The coding is literally a word by word translation of the algorithm.

```js
// function takes in two values:
// manIndex is the man proposing
// topOnMansList is the first woman on this man's list

const isAccepted = (manIndex, topOnMansList) => {
	// if the woman is unpaired (NaN true)
	// accepts proposal and registers manIndex at position 0
	// man status to true

	if (
		typeof Women[topOnMansList][0] === "boolean" &&
		!Women[topOnMansList][0]
	) {
		Women[topOnMansList][0] = manIndex;
		Men[manIndex][0] = true;
		return;
	} else {
		// if woman paired already, we loop for woman's list

		for (let order = 1; order <= Num; order++) {
			// if proposing man comes first,
			if (Women[topOnMansList][order] === manIndex) {
				// current man status back to false
				// delete this woman from his waiting list

				Men[Women[topOnMansList][0]][0] = false;
				Men[Women[topOnMansList][0]].splice(1, 1);

				// the woman dumps the current man,
				// and registers manIndex at position 0
				Women[topOnMansList][0] = manIndex;
				Men[manIndex][0] = true;
				return;
			}

			// if current man comes first
			if (Women[topOnMansList][order] === Women[topOnMansList][0]) {
				// delete this women from man's list
				Men[manIndex].splice(1, 1);
				return;
			}
		}
	}
};
```

### Final kick

In this matching function, we use `while` loop to traverse all men, find those unpaired, and send its info to `isAccepted()` for matching.

**Caution!**
You may think we can have a nested loop to find the perfect match, i.e., $n \times n$ loop. But the fact is sometimes it takes more than $n$ loops of iteration over the number of the waiting list to find the match.

I add a counter to show how many loops we need to get the result.

```js
const matching = () => {
	// at first, pairs are not matched, perfect: false
	let isPerfect = false;

	// we cannot use for loop and set loop index at array number
	// as the loop may take place more than array number
	while (!isPerfect) {
		for (let j = 0; j < Num; j++) {
			// j loop from the first to last man
			// if a man is unpaired, send man's index and top peference
			// to isAccepted()
			if (!Men[j][0]) isAccepted(j, Men[j][1]);
		}

		// isAccepted() might de-couple previous engaged pairs
		// another full loop is necessary to check all men's status

		// we presume the pairs are perfect, unless there's any unpaired man
		isPerfect = true;

		for (let j = 0; j < Num; j++) {
			if (!Men[j][0]) isPerfect = false;

			console.log(Men[j][0], isPerfect);
		}

		console.log(counter++);
	}
};
```

### An test result

```js
// men's list after match
0: (5) [true, 1, 0, 3, 4]
1: (6) [true, 3, 2, 0, 1, 4]
2: (2) [true, 4]
3: (5) [true, 0, 3, 2, 4]
4: (6) [true, 2, 3, 4, 0, 1]
```

```js
// women's list after match
0: (6) [3, 3, 2, 0, 1, 4]
1: (6) [0, 0, 1, 2, 4, 3]
2: (6) [4, 4, 1, 0, 3, 2]
3: (6) [1, 4, 1, 2, 3, 0]
4: (6) [2, 1, 3, 2, 0, 4]
```

## Proof of the algorithm

There're three points we need to discuss about the algorithm:

- **Does it terminates?** Yes, the number of men/women are finite, and the waiting list is finite. As we delete one women's name from his preference list once he is rejected by that woman, after finite round of proposals, we will either find the match, or at the end of the list.
- **Is it perfect?** Perfect means there's no one left unpaired. Now suppose we have a man and a woman unpaired. Is this situation possible? As far as the algorithm goes, the only situatioin that a woman is unpaired is that she has never received an offer. But as the left man has a whole witing list, so there's no way that the left man cannot propose to her.
- **Is the total match stable?** We assume there's an unstable pair **X-b**. The current match is **X-a** and **Y-b**. Since **X** prefers **b** over his current partner **a**, then he must have proposed to **b** before **a**. **b** either rejected **X** or accepted him first, but dropped him for another better man than **X**. Thus, **b** must prefer **Y** to **X**, contradicting our assumption that **b** prefers **X** to **Y**.

## Time complexity

We have $n$ men each with a waiting list of $n$ women. Roughly speaking, it takes $n\times n$ times for all men to propose to all women. The time complexity at worst scenario is $O(n^2)$.

But on average, the complexity is $O(n \log n)$. For detailed discussion on the time complexity topic, please refer to ["The Stable Marriage Problem" <i class="fa-sharp fa-solid fa-file-pdf fa-lg"></i>](https://drive.google.com/file/d/1vosbdHsUlBAKfXCYkRtHvNEiFelf1isr/view?usp=sharing) by William Hunt.

<br>
$$
