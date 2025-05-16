---
title: The Branch-N-Bound algorithm
description: What is it in DSA, it's characteristics and applications
tags:
  - algorithms
  - "#optimization"
---
Branch and Bound is an algorithmic technique used to solve optimization problems. it works exploring all possible solutions to a problem and dividing the problem space into smaller sub-problems.

when a set of sub-problems to the original problem space is found, some constraints (or bounds) are applied, in order to eliminate certain subproblems from consideration.

this is done to optimize the solution to the problem, reducing the search space and ensuring that subproblems that could not lead to a possible solution or to the best solution.
Branch-N-Bound uses backtracking to return to a previous node in the search tree when a dead end is reached o when a better solution is found.

some common applications of this algorithm are:
1. Traveling Salesman problem;
2. Knapsack problem;
3. Resource allocation;
etc.