---
layout: post
title: Counting Sort
date: 2022-12-9
categories: Eng
tags:
  - Algorithms
---

This post is based on two posts by [Geeksforgeeks](https://www.geeksforgeeks.org/counting-sort/) and [interviewcake](https://www.interviewcake.com/concept/java/counting-sort).

First thing first, what's counting sort?

> Counting sort is a sorting technique based on keys between a specific range. It works by counting the number of objects having distinct key values (a kind of hashing). Then do some arithmetic operations to calculate the position of each object in the output sequence.

<br>

**Characteristics of counting sort:**

- Counting sort makes assumptions about the data, for example, it assumes that values are going to be in the range of 0 to 10 or 10 – 99, etc, Some other assumption counting sort makes is input data will be all real numbers (or some items like inventory stocks that can be represented by real numbers).
- Unlike other algorithms this sorting algorithm is not a comparison-based algorithm, it hashes the value in a temporary count array and uses them for sorting. Because of this characteristic, counting sort runs in $O(n)$ time, making it asymptoticaly faster than comparison-based sorting algorithms like [quicksort](https://larry-cui.github.io/quicksort) or [mergesort](https://larry-cui.github.io/mergesort).
- It uses a temporary array making it a non-[In Place algorithm](https://www.geeksforgeeks.org/in-place-algorithm/).

<br>

**Weaknesses:**

- Restricted inputs. Counting sort only works when the range of potential items in the input is known ahead of time.
- Space cost. As this algorithm will use a counting array to store elements for further sorting, it uses up extra memory space. If the range of potential values is big, then counting sort requires extra double space as that of the original array.

<br>

**Illustration of Counting Sort:**

The algorithm can be divided into two parts, first, we count how many times each item occurs, then we build the sorted output.

**Counting**
Say we have this array, and we know all numbers in the array will be non-negative integers less than or equal to 10:

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/LdIGhQoI61T7g1I-wYZY7t8bfqORyPBr81t7SvgieT0D_ZX4whFU8fRTEbCQbU8mDZlbpEy4n0YlTwLScVP02PDqkUFL7IJ2HaW6kgx8wH5m5UNpBY_y41j2vQ6i3yAQLgfTVfCP4A=w2400" alt="counting sort"/>

<br>

The idea is to count how many 0's we see, how many 1's we see, and so on. Since there are 11 possible values, we'll use an array with 11 counters (elements), value to which are all initialized to 0.

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/ZShvxG9iwsrPc4g-AkR6rBxabAPvjpExU8txnObMxkB-jdFTG9ov_cBgwN87IlPSGeX46cYNuqlJ-FcqQHA88J90JAgKUIQnMMMfvtuzwWLihN_Tfn0_4pz3OWypv4lhyMkV8GHpCQ=w2400" alt="counting sort"/>

<br>

We'll iterate through the input once. The first item is a 4, so we'll add one to counts[4]. The next item is an 8, so we'll add one to counts[8].

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/_S9Mjvm061B3aDn272OmKH4n2dGAWPZIueOdyuGnmEyQQUDdV6uWzCgYhxGCa7fa3rpM6M81sr_taOpRhfPdfO0MIFH0qPGN0Lxzh4YmB-lj_w5s-Lb6VdALoPYNvuu3RhjBdjoBaQ=w2400" alt="counting sort"/>

<br>

And so on. When we reach the end, we'll have the total counts for each number:

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/IEnnYlLUTZn4UsFpJCvZc0VWvlgyorPWgNFzj1jIQjocA-u7Y9fDm4gfIGn8osg4rcKhI8l3RMr9trc1aW0IIo5bbJZsCv9WEg0nttualRI_fNZaI1gam-mDrOzcBm77FrI7HAcjpQ=w2400" alt="counting sort"/>

<br>

**Building**

Now that we know how many times each item appears, we can fill in our sorted array. Looking at counts, we don't have any 0's or 1's, but we've got two 2's. So, those go at the start of our sorted array.

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/uE8o7vwQmAJ7reXZcp3NT4MhL_6pYiN-HitvdTeODj7qo0NijR0WcT9ETNfqXsMYGv9Q6SE2HlMl44oEARZwZSlwZwwoFNl1VYaZpDsfcU16X51mBFSUuRuWyrc1meO_P4cKWwc49Q=w2400" alt="counting sort"/>

<br>

No 3's, but there are two 4's that come next.

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/qJeKuCP6zR6eikIV6QGN7KJny04kz88bEkAe4KFhqhilcC69f3k14J9lo7XpKh9X2rA1tQ4V7DmCOgOpS1-N4rXc_QdJSXVrsh1Y7EXs9lGoDZh5STJrxKD5xbgnDqcp6QJkFkD6dQ=w2400" alt="counting sort"/>

<br>

After that, we have one 6,

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/1PPd4pW2I8D_UZtjWrB3wITgbLnawazpOgcaG0LP-rNoR0q4id4HoFHJVftO9tH3-aKGewSRqmELbaRXqQoXAiUQJMlhqZ5Y88gpKLZ1GrhkKSH7vLd91ZePH2HlMKK2D-4z6bR21w=w2400" alt="counting sort"/>

<br>

one 8,

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/5TUUAsee4O6Y7bMuL3yo0rSPCnuGlRDnjYzJzcXWndzoeQ7WMOe8_NQ2MUF3Wzar7y9HtNZYoBqtHqUB-nKbIBRywajNDF0xJ0TTW4QZcsMj5FODWFvd924_ootU77v3RpVWMGr9fA=w2400" alt="counting sort"/>

<br>

and three 9's

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/ltLSyju3CrMHbQcxEyAhaFBc-5rYc8y503IIZ1HbEIX4Z0IPoEB6qV2fvR-d7HESjxpmOxpGxrZAtHcpmXLg6g_k-uIIUQy9U9siecgtNHxNST1i0zfo1SO0aEfK0AXzErInONwJ9Q=w2400" alt="counting sort"/>

<br>

And, with that, we're done!

<img style="display: inline-block; width: 90%; object-fit: cover;" src="https://lh3.googleusercontent.com/nqDoWsqcjPvvwrXA58BYYiD00gCdQf2DXc9a-tncAXFmUra6dSLYdL9jtgc_Lcpz0vbPAIQ-Oqskhakgscb8A3QbgZPHE8CBZTHioWHlTTbJcJk0xndP9BgHrxbOfRSVtEj5aQKGLg=w2400" alt="counting sort"/>

<br>

Below is the implementation of the algorithm:

```js
// to be provided later...
```

<br>
