---
layout: post
title: "Solution to CLRS chapter 32.3"
date: 2012-08-24 00:10
comments: true
categories: [Algorithms]
published: false
---

## Problem 32.3-3

> We call a pattern P nonoverlappable if Pk ⊐ Pq implies k = 0 or k = q. Describe the state-transition diagram of the string-matching automaton for a nonoverlappable pattern.

In each state there will be only one transition to the next state, and all the other transitions lead back to the initial state 0.

## Problem 32.3-4

> Given two patterns P and P′, describe how to construct a finite automaton that determines all occurrences of either pattern. Try to minimize the number of states in your automaton.

The most naive one I can think of is to find first divergence of the two patterns, assume it is at *k*, which means Pk equals to P'k, and build a automaton for Pk. Then the next characters of the two patterns will diverge, each leads to another automaton, which is built on the left part of the pattern.

To minimize the number of states, we may use algorithms that reduce