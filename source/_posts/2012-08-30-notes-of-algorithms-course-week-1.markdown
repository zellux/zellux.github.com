---
layout: post
title: "Successor with Delete"
date: 2012-08-30 10:05
comments: true
categories: [Algorithms]
---

## Problem
Given a set of N integers S={0,1,...,N−1} and a sequence of requests of the following form:

- Remove x from S
- Find the successor of x: the smallest y in S such that y≥x.

design a data type so that all operations (except construction) should take logarithmic time or better.

## Solution

This is a problem taken from the interview questions in union-find set on [Coursea Algorithms Course](https://class.coursera.org/algs4partI-2012-001/quiz/attempt?quiz_id=89).

It would be much harder if posted to the interviewee without context of union-find set. Fortunately we now known it can be solved with union-find set.

The results of finding the successor of x are saved in union-find sets, that is, when finding the successor of x, we simply return the root of the set containing x. When removing x from S, we need to make successor of removed numbers consequent to x and before x as that of x + 1. This is exactly what union function needs to do. To remove x from S, we simply merge the set containing x to the set containing x + 1 (append as its child). 

This will work for both removing and finding except that in worst cases it does not run in logarithmic time, since it does not consider set weight when merging two sets. To opmitize this, our merging function will work in a way similar to weighted quick union, except that if the numbers in the larger set are smaller than that in the smaller one, we need to change the root of unioned set to the root of the larger set. This can be done by changing the original root of the two sets. Then we make ensure logarithmic time in worst case.
