---
title: The Branch-N-Bound algorithm
description: What is the Branch-N-Bound in DSA, it's characteristics and applications
tags:
  - algorithms
  - "#optimization"
---
Branch and Bound is an algorithmic technique used to solve optimization problems. it works exploring all possible solutions to a problem and dividing the problem space into smaller sub-problems.

when a set of sub-problems to the original problem space is found, some constraints (or bounds) are applied, in order to eliminate certain subproblems from consideration.

this is done to optimize the solution to the problem, reducing the search space and ensuring that subproblems that could not lead to a possible solution or to the best solution.
branch and bound uses backtracking to return to a previous node in the search tree when a dead end is reached o when a better solution is found.

a branch and bound algorithm provide an optimal solution to an NP-Hard problem by exploring the entire search space. through the exploration of the entire search space, a branch and bound algorithm identify possible candidates for solutions step-by-step.

these algorithms are used to find the optimal solution for combinatory, discrete and general mathematical optimization problems, such as:
1. Traveling Salesman problem;
2. Knapsack problem;
3. Resource allocation;
etc.

they incorporate different search techniques to traverse a state space tree, such as [BFS](https://github.com/guisaliba/dsa/blob/main/algorithms/search/graphs-search/bfs/notes.md), [DFS](https://github.com/guisaliba/dsa/blob/main/algorithms/search/graphs-search/dfs/notes.md) and [LC]().

the algorithm uses upper and lower bounds to cut down on the size of the search area. this has proven to be successful in locating the best solutions to challenging optimization problems.

it starts with an initial lower bound and iterations improve it until an optimized solution is found.

however, it's worst case time complexity is exponential in the size of the input ($O(n^2)$) and it uses a lot of memory in order to store the search tree and the current best answer to the problem.

the quality of the problem-specific constraints determines how well this technique performs, meaning that the harsher the bounds, the worser it's performance might be.