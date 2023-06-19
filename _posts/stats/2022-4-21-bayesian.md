---
layout: post
title: Bayesian Estimation
date: 2022-4-21
categories: Eng
tags:
  - Stats
---

Even if we can pick the correct pdf model for the whole population of data, we may never know
the true parameters for such models. We construct different kinds of functions to evaluate the
parameters, which we call point estimators. We feed sample data to the function and get the
result, i.e., estimate(s), for the true parameter(s). Apparently, if we have different sets of samples, we would have different estimates.

The spread out of the estimates is itself a probability density. If the function/estimator is
simply the sum or mean of the sample, we know from the CLT that estimates will follow a
normal distribution pattern, with a mean of $\mu$ and variance of $\sigma^2$.

When new data sample flows in, it presents an opportunity to check and update our estimates
to catch up with the development of whole data conveyed by such new samples. Do we need
to combine “old” and “new” data and use bothersome maximum likelihood or moments methods
to re-calculate the estimates? Of course you can do that. But we have a better solution with help from
Bayesian estimation, and new tools about model functions for parameter estimates.

<a href="/pdf/bayesian.pdf" target="_blank">Read more</a>
