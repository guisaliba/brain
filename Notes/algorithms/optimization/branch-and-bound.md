---
title: The Branch-N-Bound algorithm
description: What is the Branch-N-Bound in DSA, it's characteristics and applications
tags:
  - algorithms
  - "#optimization"
---
branch and bound is an algorithmic technique used to solve optimization problems. it works exploring all possible solutions to a problem and dividing the problem space into smaller sub-problems.

when a set of sub-problems to the original problem space is found, some constraints (or bounds) are applied, in order to eliminate certain subproblems from consideration.

this is done to optimize the solution to the problem, reducing the search space and ensuring that subproblems that could not lead to a possible solution or to the best solution.
branch and bound uses backtracking to return to a previous node in the search tree when a dead end is reached o when a better solution is found.

a branch and bound algorithm provide an optimal solution to an NP-Hard problem by exploring the entire search space. through the exploration of the entire search space, a branch and bound algorithm identify possible candidates for solutions step-by-step.

the algorithm uses upper and lower bounds to cut down on the size of the search area.

these algorithms are used to find the optimal solution for combinatory, discrete and general mathematical optimization problems, such as:
1. Traveling Salesman problem;
2. Knapsack problem;
3. Resource allocation;
etc.

they incorporate different search techniques to traverse a state space tree, such as [BFS](https://github.com/guisaliba/dsa/blob/main/algorithms/search/graphs-search/bfs/notes.md), [DFS](https://github.com/guisaliba/dsa/blob/main/algorithms/search/graphs-search/dfs/notes.md) and [[LC]]. the order in which the state space tree is searched classifies the branch and bound method.

B&B generates a state space tree to efficiently search the solution space of a given problem instance.

in B&B, all children of an E-node in a state space tree are produced before any live node gets converted in an E-node. thus, the E-node remains an E-node until it becomes a dead node.

it starts with an initial lower bound and iterations improve it until an optimized solution is found. this is achieved by applying a bounding function at each iteration on the possible solutions at each node.

a **bounding function** is a heuristic function that evaluates the lower and upper bounds on the possible solutions at each node. if a node does not produce a solution better than the current best solution, it is abandoned without further exploration.

the algorithm then branches to another path to get a better solution. the desired solution to the problem is the value of the best solution produced so far.

there are two ways to represent a branch and bound algorithm solution:
1. variable size: if we have to select a combination of elements from `{A, B, C, D}` that optimizes the given problem, and it is found that A and B together give the best solution, then the solution will be `{A, B}`.
2. fixed-size: represented by 0s and 1s where 1 represent that we select the element which at nth position and 0 represent that we don't select the element at the nth position. for the above example, the solution would be given by `{1, 1, 0, 0}`.

visualizing an exploration of a state space tree using the [[LC]]-branch and bound:
in this technique, nodes are explored based on their cost. the cost of a node can be defined with the help of the given problem, thus defining a cost function.

once the cost function is defined, the cost of each node can be defined. let's consider the diagram below.
![[111.webp]]

in this method, node C will be explored since it has the minimum (least) cost. during exploration of node 4 which is element C, there is only one possible element that remains unexplored, which is D.

so node C will get expanded to one single element D. let's say this node number is 6.
![[222.webp]]

now node 6 has no element left to explore, so there is no further expansions. hence, the element `{C, D}` is the optimal way to choose for the least cost.

however, it's worst case time complexity is exponential in the size of the input ($O(n^2)$) and it uses a lot of memory in order to store the search tree and the current best answer to the problem.

the quality of the problem-specific constraints determines how well this technique performs, meaning that the harsher the bounds, the worser it's performance might be.