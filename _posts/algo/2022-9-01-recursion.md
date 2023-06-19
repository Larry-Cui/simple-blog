---
layout: post
title: Recursion
date: 2022-09-01
categories: Eng
tags:
  - Algorithms
---

As mentioned in other posts before, recursion is just a coding technique, not fancy as it sounds at all.

Let's take a look at a recursion example:

```js
// find GCD (greatest common dividor)
// using recursive coding method

const gcdFind = function (a, b) {
  // roll back condition
  if (a === b) return a;
  else return a > b ? gcdFind(a - b, b) : gcdFind(a, b - a);
};
```

All loop functions can be coded otherwise in recursive method, and all recursive can be changed back to loop function.

We can tell some features of the recursive coding:

- a recursive function will call for itself inside its function scope.
- we need to provide a stop and roll back condition for a recursive function, otherwise it will loop forever.
- we use `return` to jump out of one loop, but as recursive is one loop inside another, we need `return` for each loop, not just the inner-most loop (roll back loop) .

The key to understand recursive function is practice. Here we end this post with another example.

Recursive function to find $n!$:

```js
const factorial = (n) => {
  return n === 0 ? 1 : n * factorial(n - 1);
};
```

We need to elaborate a bit about the above code. First of all, we are using a simplified `if` condition.

```js
// usually if condition
// when the actions on true or false
// have more than one line instrucitons
if (n === 0) {
  console.log("more actions");
  return 1;
} else {
  console.log("more actions");
  return n * factorial(n - 1);
}
```

```js
// when there's only single action,
// we don't need curly brackets
if (n === 0) return 1;
else return n * factorial(n - 1);
```

We can further simplify `if` as follows. Here actions on true and or false are separated by colon.

Be noted that `return` is not needed in the simplified one line `if` condition, as this is a default setting to return the value of whatever following the `?`.

```js
n === 0 ? 1 : n * factorial(n - 1);
```

However, sometimes we need be very careful: as the out-most loop of a recursive returns the result to the **function itself**, not out of the function, when we call the function, we need an extra `return` to force the function to regurgitate the result.

```js
return n === 0 ? 1 : n * factorial(n - 1);
```

<br>
