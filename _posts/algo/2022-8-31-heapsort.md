---
layout: post
title: Heap Sort
date: 2022-08-31
categories: Eng
tags:
  - Algorithms
---

**Table of Contents:**

- [Definition and categories of heaps](#definition-and-categories-of-heaps)
	- [index and height of a heap](#index-and-height-of-a-heap)
	- [Max and min heaps](#max-and-min-heaps)
- [Insert an element to a heap](#insert-an-element-to-a-heap)
	- [Algorithem in normal language](#algorithem-in-normal-language)
	- [Code example](#code-example)
	- [Time complexity of heap insertion](#time-complexity-of-heap-insertion)
- [Create a heap](#create-a-heap)
	- [Time complexity](#time-complexity)
- [Heapify: a faster method to create heap](#heapify-a-faster-method-to-create-heap)
	- [Time complexity of heapify method](#time-complexity-of-heapify-method)
- [Deleting from Heap](#deleting-from-heap)
	- [What we get from deleting the heap array?](#what-we-get-from-deleting-the-heap-array)
- [Heap Sort: best for priority queue](#heap-sort-best-for-priority-queue)
	- [The power of heap sort](#the-power-of-heap-sort)

## Definition and categories of heaps

Heap sort is based on a heap. What is a heap? simply put, it's a way of array order. As heap is not common to our daily life, it's worth to elaborate a bit about the structure of heap.

Heap is a binary tree of numbers, and it a complete one, the definiton/features of which include:

- nodes cannot have any child if their siblings are not filled yet;
- at the same level, if not all nodes are filled with children, then left-side nodes must be filled first;
- no child should be appended to any nodes until the nodes of the same level are filled with numbers.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/31mkKeg9OeglKgBvg5-BMSJ2vCx5L5iDKna1TEZ_rqlI_Z12fJyXhAujLXkq3MSP7QFSVf0AErnNAK4lnskFCNBAnemMmYPD0vIK5ipFDNgjZiJ6fKfydNAJpNgPpNZLjKgHF3KmxA=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Complete and Non-complete Binary Tree Illustration</div>

<br>

### index and height of a heap

You may have noticed the index order of the binary tree. It's top down and left to right. There's a mathematical connection between a node and its children. For the ease of calculation, we define the first (top) node of a binary tree at index 1.

**For node at index i:**

- left child at: $2i$
- right child at: $2i +1$

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/HIe-6tKQGQmaGpbeWDlVJDZBHWR7Jer0HboHhtWnRHoA99g0kqhebtV6rpZ_QJrNefbSaEIU92UB4ZEd2ozZNlhT4poI698aUZft4Gtyz6i-bQyZPgMXHvDrrQtv0fDGNmrcMNzApA=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Index of a Heap Tree Illustration</div>

<br>

**For n number occupying an complete binary tree, its height of nodes:**

- $\log_2 n$

### Max and min heaps

Just as any sorted array can be in a ascending or descending order, so does a heap, but in a slight different way, i.e., max heap and min heap:

- In a max heap, every node is greater or equal than its children, while in a min heap, every node is less than its children.
- Nodes at the same level, siblings, are not necessarily in order.
- it's premitted that some children of one node is greater (in max heap) or less (in min heap) than their uncles.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/GKKmQdl8Awvr09vsgfebsfGGysmnvi3ZUvTWRaetU9twz3P5Rc_YI9_pQrxDVJL-OVz06-nepcpxidk1sc5Sz4gn_83NKIVJxX4yWUvBS0YQmkOR6jxNkfBg-fO59JJSNVSZwVNIsA=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Min Heap (left) and Max Heap (right)</div>

<br>

**Heap is not for searching purpose!**

## Insert an element to a heap

First of all, we record the elements of a heap in an array, in an order as describe above, i.e, starting with the top node as index 1 (or index 0 in JavaScript), then the second layer of nodes as index 2 and 3, then the third layer as index 4-7, and so on.

### Algorithem in normal language

Let's use min heap as an example.

- We always start by adding the new element to the end of the array.
- Next, we compare the new element with its parent node, if the parent is greater than the new element, swap.
- Now the new element is in the swapped index, compare it with the upper parent again, swap by the same rule.
- If the new element is less than its parent, or it's already at the top node, insertion finishs.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/SbrcDlWdPtXXWdqJ_THOFYLeROkhtUzR_eTonF0CKKkZaTcK3X6a1wF3rYQyQ38-1bsxTUeig1rEwaMER_fG-ggxCSMAyx9nOFYRGBhTM2-4CeMDNIU4Bk95EmWxPIEYnA9vgUiL-A=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Inserting to a Min Heap Illustration</div>

<br>

### Code example

Now let's try code the algorith of heap insertion by JavaScript. Here we're using a technique called recursion, and also be noted that this is a max heap.

```js
// Heap Insertion

// we need a swap function
const swap = (arr, a, b) => {
	const temp = arr[a];
	arr[a] = arr[b];
	arr[b] = temp;
};

// recursive coding
const insertRecur = (array, index, n) => {
	// since JavaScript array starts from 0, we need some adjustment
	const parentNodeIndex = Math.floor((index - 1) / 2);

	// roll back condition of the recursion
	if (array[parentNodeIndex] >= n || index === 0) return array;

	swap(array, parentNodeIndex, index);
	index = parentNodeIndex;

	// recursion bichotomy point
	insertRecur(array, index, n);
};

// with swap and insertRecur function
// we only need to pass info and call these functions
const insertHeap = (array, n) => {
	array.push(n);
	const index = array.length - 1;
	insertRecur(array, index, n);
	return array;
};
```

### Time complexity of heap insertion

The insertion procedure takes at most as many steps as the height of the heap binary tree, so the time complexity is $\log n$ (short for $\log_2 n$).

## Create a heap

After we know how to insert new element to a heap, it comes intuitively that we can create a heap by inserting elements to a new array one by one. As a matter of fact, if we are given an un-ordered array and asked to create a heap using these element, we can work within the same array and do some compare and swap jobs as insertion algorithm demands.

Here below is the code practice for creating a heap. For ease of reference, I use a new array instead of working on the origianl one.

```js
// Create a heap array
// we are re-using insertHeap function from above

const heapArray = (n) => {
	const array = new Array();
	for (let i = 0; i < n; i++) {
		// here we use numbers by random funtion,
		// we can of course use other sources.
		let element = Math.round(Math.random() * n * 3);

		insertHeap(array, element);
	}
	return array;
};
```

### Time complexity

If we observe from the stand point of the last element, it takes at most $\log n$ steps to insert to the heap. As we have $n$ elements in total, so the worst scenario is $n \log n$.

## Heapify: a faster method to create heap

There's a clever way to sort the array into a heap without doing insertion one by one, this is called heapify. We will walk through an example to illustrate the algorithm. This example is from [Subham Datta's post](https://www.baeldung.com/cs/binary-tree-max-heapify), and again we are using max heap instance.

Here we have an array: $[10, 20, 25, 6, 12, 15, 4, 16]$, the binary tree is like this:

<div style="display: flex; justify-content: center">
<img style="display: inline-block; width: 50%; object-fit: cover;" src="https://lh3.googleusercontent.com/dvWw_pPjWVuclJ0nKa9PsfRCWLYe4nEJBR_lR7h3uQekMd809PeXWPlk0oNNTyoIjqeh-Xf1TGGYg-ufFbdEOJPwXsxt3_l5uAVXc_0rb1I7-DJasRWADn0ymcHi6vm-Ww0lxf2Bhw=w2400" alt="insertion sort"/>
</div>

<br>

**1.** Heapify is a leaf to root process. Check out all leaves at the bottom, nothing is below them, so they are heapified by defintion. now check out the one level above the leaves. We see "6" is less than its child "16", so swap.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/ntyvYSvybYRXXMEShDTkKWSorRXvcYMCKXQS3XUdJzSaiBVEuzE2p2GAcSAiYs5w-_Y3LBdKxLyN5VwXH0yFKnYb5JQWCYIExjeM2wLPCnBPEoGNJ771TyTwgrB8pM0vlG9LB-l5lA=w2400" alt="insertion sort"/>

**2.** look at one level above, number "20" has two children "16" and "12", they are both less "20", so nothing happens here.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/fb9jCcAaFjmOjT5iVVJ-7A7_Rd3XBeFaBA5nyLtGtxijEC3rcq4bi3no2jVYQqucCTwMLPt2_M7lE0lxqkuzqkG6JBvEBIrvz05aEocrlPy1-gvuhnV-Ydz_UcRiXWy0Dh-DP0NOPQ=w2400" alt="insertion sort"/>

**3.** look at another sibling at the same level, number "25" has two children "15" and "4", nothing happens either.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/kNdIzOkkhPMMsHaD5mBl5NjKlbHGyQyYlgEowj05q-eHqnDG4s2ZagHkrX2Q4jJMSCyKCv8NeZDEAgXwEhRDrGM35PK0dNW21TdksZE0V2iLkyrvAjPeYLLM1e_6Q-NGtfJKR8TUgQ=w2400" alt="insertion sort"/>

**4.** Now we reach at the root. Apparently, root "10" is less than its children, but we pick the larger one "25" and swap with "10".

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/UJAmV5We8_aaeVD7QbAprsBGOHHZjFqQ7b2Q40t4bJED-EWb3VGvvt-NGSxqrCLOBbgWT53kuIofyIcIw0Rrr41UUwqzCuv-BIrXTUocfzlBzm-k3lfpXat3Rwa9Ap4x_xLNYGVtLg=w2400" alt="insertion sort"/>

**5.** We need to keep an eye on the swaped down element closely. We need to check if it's still smaller than its children in the new position, if not, swap doan again. Here we swap "10" with "15" to make sure it keeps on the right position.

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/zyH62HVXxk-gVMCZRuGGaCrV7Qq2upTprx_Vhq_BCw31SGb_-2tLJm1gFLt-Sfy_z5MW0Gt9keGL-cmYwo6txSqRGCDkEd2_ZaI6IOfc0PCbVhZXQhcruf1haIap_cFaMo8IZ62VIQ=w2400" alt="insertion sort"/>

### Time complexity of heapify method

We know the bottom leaves are always good as there are no children below them, which takes half of the total number of elements, $n/2$. For the first floor of the nodes, which has $n/4$ in total, will need to be brought down to leaves for one floor distance at the worst scenario. For the second floolr, the number of nodes comes to $n/8$, and distance is 2.

The total moves at worst:
$$S = \left(0*\frac{n}{2}\right)+\left(1*\frac{n}{4}\right)+\left(2*\frac{n}{8}\right)+ \cdots + \log n * 1$$

Now we need some calculus skill here:

$$
\begin{align*}
S&= \sum^{\log n}_{k=1} \frac{kn}{2^{k+1}} = \frac{n}{4} \sum^{\log n}_{k=1} \frac{k}{2^{k-1}}
<  \frac{n}{4} \sum^{\infty}_{k=1} \frac{k}{2^{k-1}} \end{align*}
$$

If we let $x=1/2$, the right most term can be written as:

$$
\begin{align*}
\frac{n}{4} \sum^{\infty}_{k=1} \frac{k}{2^{k-1}} &= \frac{n}{4} \sum^{\infty}_{k=1} kx^{k-1} \\
&= \frac{n}{4} \frac{d}{dx} \left[\sum^{\infty}_{k=1} x^k \right] \\
&= \frac{n}{4} \frac{d}{dx} \left[\frac{1}{1-x} \right] \\
&= \frac{n}{4} \frac{1}{(1-x)^2} \\
&= n
\end{align*}
$$

So we conclude the complexity is $O (n)$.

## Deleting from Heap

It seems opposite to intuition, but the rule of heap deleting is, you can only delete the root element. In max heap, this is the largest element, in min heap, the smallest.

The procedure of the algorithm goes as follows (max heap):

- delete the first element (root) from the heap array
- now move the last element of the heap array to the root position, which is at index 0 in JavaScript
- compare root's two children, find the larger one, and swap position of the larger one with the root element if the child is larger than the root element (Remember: the root element is the element swapped from the last position of the array)
- go all way down with the root element, until it's larger than its children.

<br>

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/AjqdbpX0Po2EwlLfYuzkqWxD9tqpISHy3kKMTFHT_XZWmJRY82DZz7FbhSFRj6DNUoZjpgjTPoBvOygogOaMapRJzYDZdqBllrgURFIBuM1ZB1aL16l8dH2ytUbuu301XhUPLRHJIA=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Step 1: "21" is the last of the heap array</div>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Step 2: delete "45", and move "21" to the root position</div>

<br>

<img style="display: inline-block; width: 100%; object-fit: cover;" src="https://lh3.googleusercontent.com/X5Uo8tmqD0gIzyeUm4kah93zWuk8yxVCLzUdCwoGKRUIWnhLZfEii8z8H2IqRCSDtLXsuDGKE-hq0-q6xhK55z4nsbSAHi-szEJk601wG_OFkg3Q8G82ZStfAbroBQMNgiJ3GgZrxg=w2400" alt="insertion sort"/>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Step 3: compare children of "21", "42" is larger than "23", so swap "42" with "21"</div>
<div style="display: flex; align-items: flex-start; justify-content: center; font-size: 14px; color: #777;">Step 4: repeat step 3, child "35" is larger than "27", swap "35" with "21"</div>

<br>

After step 4, "21" has no child, we can stop the procedure, the new heap array is sorted.

Code practice here in JavaScript.

```js
// swap function is here to help swap elements
const swap = (arr, a, b) => {
	const temp = arr[a];
	arr[a] = arr[b];
	arr[b] = temp;
};

// we use recursive again!
// the array this heapify function takes in
// is a heap array except the first element swapped from the last
function heapify(arr, i) {
	// because JavaScript array starts from 0
	// left child is 2 * ( i + 1 ) - 1 = 2 * i + 1
	// right child is 2 * (i + 1 ) + 1 - 1 = 2 * i + 2
	let l = 2 * i + 1;
	let r = 2 * i + 2;

	// roll back conditions for heapify recursive function
	if ((arr[i] > arr[l] && arr[i] > arr[r]) || r > arr.length - 1) return arr;

	// compare child first, then use the larger child to compare with parent
	if (arr[l] > arr[r]) {
		if (arr[l] > arr[i]) {
			swap(arr, l, i);
			i = l;
		}
	} else {
		if (arr[r] > arr[i]) {
			swap(arr, r, i);
			i = r;
		}
	}

	// Recursively heapify the affected sub-tree
	// notice "i" has been changed to its child node index
	heapify(arr, i);
}

// Function to delete root and
// send array to heapify for further process
function deleteRoot(arr) {
	// get the root
	const root = arr[0];

	// splice comes back with an array,
	// so we need to get the number out of it
	arr[0] = arr.splice(-1, 1)[0];

	// heapify(sort) the array
	heapify(arr, 0);

	// return heapified array and the deleted root
	console.log("Deleted root is: " + root);
	return arr;
}
```

### What we get from deleting the heap array?

Yes, we get an ordered list of numbers. From max heap, we get the numbers in a descending order, and from min heap, we get the numbers in an ascending order.

## Heap Sort: best for priority queue

Now we have all the bricks for a heap sort algorithm. To implement heap sort on an un-ordered list of numbers:

1. create a heap array by inserting;
2. delete root of the heap array one by one and copy it somewhere else to get an ordered list of numbers.

The time complexity is $n \log n $ for each step, so the total is $2n \log n$, but in practice we still call it $n\log n$.

### The power of heap sort

Suppose you are running a service center. Calls for help coming in every day at different priority level. You need to record each call and dispatch your engineers to meet requirments from those with higher priorities first. How do you register and organize the calls?

You can do it in a linear way:

- you take notes for each call and just keep them in the order as the time they came in. The time complexity for each registration is $O(1)$.
- when your next engineer is available, you do a linear search of your registration book and find the entry with the highest priority. It takes a time complexity of $O(n)$.

Or you can do it with heap array:

- you insert each incoming call into your existing heap array (max heap for example). How much time does it need? $O(\log n)$ for heap insertion.
- when dispatch, you take the root out of the heap, and modify the array to keep it in a proper manner. How much time does it need? $O(\log n)$ for heap delete.

**In conclusion, heap structure is best for priority queue.**

<br>
