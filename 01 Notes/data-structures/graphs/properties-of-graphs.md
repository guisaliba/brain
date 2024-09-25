an edge can be called a **self-loop** if it envolves only 1 vertex. a page in the web is an URL, it can contain links to other pages, but it can also contain a link to itself. that's a clear example of a self-loop.

another special type of edge is **multi-edge**, or **parallel edge**. an edge is a multi-edge if it occurs more than once in a graph, that is a vertex u that has two directed edges connecting it to a vertex v, they are the same ordered pair: (u, v) but two different edges.

if a graph contains no self-loops or multi-edges it is a **simple graph**.

the minimum possible number of edges in a graph is **zero**, because a graph is still a graph even if there are no edges linking its vertices.

the maximum number of edges in a digraph is:
	N * (N - 1)

for undirected graphs, the maximum number of edges would be:
	N * (N - 1) / 2

number of edges can be really larger than number of vertices in a graph.
let's say N = 40, then the maximum number of edges in a digraph would be:
	40 * (40 - 1) = 1560 edges

for an undirected graph, that number would be 780.

a graph is called dense if there are too many edges compared to vertices, and it is called sparse if there are too few edges in comparison.

we tipically store dense graphs in a structure called adjacency matrix, and sparse graphs in a structure called adjacency list.

a path is a sequence of vertices where each adjacent pair is connected by an edge. we can represent them like: A, B, F, H. which means there is an edge linking vertex A to B, another from B to F, and another from F to H. this is a path A -> B -> F -> H.

a simple path is a path in which no vertices and edges are not repeated. the above path is a simple path, because no vertices and edges were repeated. it can also be called a walk.

a walk is called a trail if vertices can be repeated but edges can not.

a graph can be a strongly connected graph if there is a path from any vertex to any other vertex. for undirected graphs, if there is a path from any vertex to any other vertex, we call it connected.

for a directed graph that satisfies this condition, we call it strongly connected. 

a walk is called a closed walk if it starts and ends at the same vertex. the length of a walk is the number of edges in the path. in the above example, the length of that walk is 3, which is not a closed walk (it does not start and end at the same vertex).

a cycle is nonetheless a closed walk. a graph with no cycle is called an acyclic graph, e.g.: a tree with undirected edges (parent-children relationship can never form a cycle because one can not be a child of their parent and parent of their parent at the same time).

a directed acyclic graph is often called a DAG.