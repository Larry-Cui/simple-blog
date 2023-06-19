---
layout: post
title: Bucket Sort
date: 2022-12-9
categories: Eng
tags:
  - Algorithms
---

This post is based on [Geeksforgeeks]([https://www.geeksforgeeks.org/radix-sort/) and [Javapoint](https://www.javatpoint.com/bucket-sort).

Bucket sort is mainly useful when input is uniformly distributed over a range. By custom, this range usually is from 0 to 1.

For example, consider the following problem:

Sort a large set of floating point numbers which are in range from 0.0 to 1.0 and are uniformly distributed across the range. How do we sort the numbers efficiently?

A simple way is to apply a comparison based sorting algorithm. But they cannot do better than $O(n \log n)$. Can we sort the array in linear time? Counting sort can not be applied here as we use keys as index in counting sort. Here keys are dsicrete floating point numbers.

The idea is to use bucket sort.

> Bucket sort is a sorting algorithm that separate the elements into multiple groups said to be buckets. Elements in bucket sort are first divided into groups called buckets, and then they are sorted by any other sorting algorithm. After that, elements are gathered in a sorted manner.

The basic procedure of performing the bucket sort is given as follows:

- First, partition the range into a fixed number of buckets.
- Then, toss every element into its appropriate bucket.
- After that, sort each bucket individually by applying a sorting algorithm.
- And at last, concatenate all the sorted buckets.

**Note:** step 3 above is not necessarily to carried out separately after step 2. In fact, if you choose insertion sort, the sorting work can be done at the same time as you toss an element into the corresponding bucket.

**Pros**

- Bucket sort greatly reduces the no. of comparisons by dividing elements into small groups (buckets).

**Cons**

- Becasue it is not an in-place sorting algorithm, it needs some extra huge memory space when comes to large array. So it's costly in terms of space.

**Illustration of Bucket Sort on Floating Numbers**

In fact, we will let the number of buckets (n) be as many as the array length. The benefit of this practice is, if the array is uniformly dispersed, then element would fit into buckety quitely evenly, passing less job for further sorting within each bucket.

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/ASopf72CgyON9UB_RtI0RVUFaCs_ZpMwpXfL1bedu-DEN3dBPX8D5QNW3Dj4_xo1fT6YpL7rJ9x63lXxC7UH7g7DPj8_prNh9qOir6l-jLm7eH7VT6n_3sauQGnUVIt7DDz4fIshuA=w2400" alt="bucket sort"/>

<br>

As you can see from the above illustration, the auxilliary bucket array is the same length as the original array.

**Illustration of Bucket Sort on integers**

Of course, bucket sort can also be used to integers, in which case, we can choose a bucket number as we see most adapted to the given array.

Given an array $[10,8,20,7,16,18,12,1,23,11]$. Based on the maximum number, we can roughly create buckets with a range from 0 to 25. The buckets range are 0-5, 5-10, 10-15, 15-20, 20-25. Elements are inserted in the buckets according to the bucket range. Suppose the value of an item is 16, so it will be inserted in the bucket with the range 15-20. Similarly, every item of the array will insert accordingly.

The following phase is known to be the **scattering of array elements**.

<img style="display: inline-block; width: 80%; object-fit: cover;" src="https://lh3.googleusercontent.com/ZxR8hC9IcynnX9QgSZAxtMmWg9LTMMR52OFVHgYcVSQtYYe8tjxxA9CgoQ51Keu__gj-hzZ-G86JJSZ9PFLxyZHpB0qxNTLg7cjFaYElCZu05MW9qIahfsuYny1Nwx2J8-No1c-6eQ=w2400" alt="bucket sort"/>

<br>

Now, sort each bucket individually. The elements of each bucket can be sorted by using any of the sorting algorithms.

<img style="display: inline-block; width: 80%; object-fit: cover;" src="https://lh3.googleusercontent.com/zoPLwL9xGG2CsWxsoF0zDeBwrT6bQhkPhAvVqb1w0_63THJw9b4xGnWnOpee1Qn2qGJCuDhR5_A729ZOZsTqS45G9HKDguJYXYn_jmX50bZnUJZi_kqmrTubWUrqHhiQrB6WPLPOLg=w2400" alt="bucket sort"/>

<br>

At last, gather the sorted elements from each bucket to complete the sort.

**Time Complexity**

- **Best Case Complexity** - It occurs when there is no sorting required at bucket level, i.e. the array is already sorted. The best-case time complexity of bucket sort is $O(n + k)$. $k$ here is the bucket number.
- **Worst Case Complexity** - In bucket sort, worst case occurs when the elements are of the close range in the array, because of that, they have to be placed in the same bucket. So, some buckets have more number of elements than others. As we have no good way than comparison-based algorithm to sort elements in a bucket, in the worst-case time complexity of bucket sort is $O(n^2)$.

<br>
