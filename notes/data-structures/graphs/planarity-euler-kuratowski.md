#  graph's planarity refers to the property of a graph being planar. 

this means checking whether a graph can be represented in a two-dimensional plane (like a paper or a sheet) without edge crossings.

a planar graph is a graph that can be drawn on a two-dimensional plane in such a way that its edges intersect only at their endpoints. in other words, no edges cross each other except where they meet at a common vertex (endpoint).

## visual example:
imagine drawing a triangle, or a square. you can easily draw each of their three and four edges respectively without any of them crossing each other. triangles and squares are a simple example of a planar graph.

## non-planar example:
consider the graph $K5$  which is a **complete** graph (a graph where every pair of distinct vertices is connected by a unique edge). it cannot be drawn on a plane without some edges crossing thus making it a non-planar graph.

there are several methods and theorems to determine the planarity of a graph:

## Kuratowski's Theorem
**Theorem (Kuratowski, 1930):** _A finite graph $G$ is planar **if and only if** it does not contain a subgraph that is a subdivision of $K5$ (the complete graph on five vertices) or $K3,3$​ (the complete bipartite graph with partitions of three vertices each).

a graph is planar if and only if it does not contain a subgraph that is a subdivision of either $K5$ (the complete graph of five vertices) or $K3,3$ (the complete bipartite graph on two sets of three vertices).
- if you can find a $K5$ or a $K3,3$ within your graph, the graph is non-planar
- if neither exists, the graph is planar.

## Euler's Formula
is a relationship between the number of vertices ($V$), edges ($E$) and faces ($F$) in a connected planar graph:
$$ V - E + F = 2 $$
- if a graph satisfies Euler's formula and does not contain $K5$ or $K3,3$ as a subgraph, it is planar.

## determining planarity

1. Check for $K5$ or $K3,3$
2. Apply Euler's Formula
3. Attempt to draw the graph.

if $K5$ or $K3,3$ is found, that is, a complete graph of five vertices or the the complete bipartite graph on two sets of three vertices is found, it is not planar.

if neither of these are found and applying Euler's Formula evaluates to be true, then it the graph is planar.