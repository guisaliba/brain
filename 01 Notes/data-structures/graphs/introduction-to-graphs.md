just like a tree, a graph is a non-linear data structure. it is a collection of **entities** called **nodes or vertices** connected by **edges**.

in a tree there are rules dictating those vertices. first of all, vertices and edges represent parent-child relationship. an edge connects two nodes and sets the hierarchical structure of parent-child.

if a tree has N nodes, then the number of edges is exactly N -  1, because all nodes have at least one parent except for the root node. edges connect parents to their children thus the root node not having a parent means it has no edge coming from another node to it, so N - 1.

also, in a tree any node must be reachable from the root by exactly one path. this means that if a node V belongs to a tree, there has to be one path from the root that reaches V.

for graphs, there are no rules dictating the connection among the nodes.
edges can connect a set of nodes in any way.

a tree is a special kind of graph.

a graph **G** is an ordered pair of a set **V** of vertices and a set **E** of edges.
	**G = (V, E)**

an ordered pair means that (a, b) is different from (b, a) if a != b.
"a" must always be a vertex and "b" must always be an edge.

we usually name vertices in a graph, like: V = {V1, V2, V3, V4, V5} for a graph with 5 vertices for example. for edges, they can be identified from their two endpoints. if an edge connects a vertex u to a vertex v, we can just write: u --- v to represent that edge.

edges can be of two types:
1. directed: u -> v, means that there is a path from u to v but we can not assume a path from v to u, this can be represented like: (u, v)
2. undirected: here the connection is bi-directional. origin and destination are not fixed, we only need to know what endpoints are being connected. we can represent them like:  {u, v}

a directed graph, which has all directed edges is called a **digraph**.
a graph with all undirected edges has no special name.

graphs representations:
1. social network: a social network can be represented by an undirected graph, where each vertex is a person and the edges represent a connection between them, let's call it a friendship. it's an undirected graph because a friendship is a 2-way connection: if i am friends to someone, they are also friends of mine.
2. world-wide-web: the web can be represented by a graph because pages can be linked to other pages. so the vertices of this graph would be pages and the edges would represent links: an edge connects two vertices only if one of them links to the other one. in other words, this is a directed graph, the relationship is not mutual this time, a page can link to another one that doesn't link back to it.

we can apply standard graph theory algorithms to solve problems. for the web example, a famous algorithm that can be applied is web-crawling.
web-crawling is basically graph traversal, or in simple words, the act of visiting all nodes in a graph.

graphs can be weighted, because sometimes in a graph all connections can not be treated as equal. for example, the highways between cities can have different lengths. again: vertices are cities and edges are the roads, and since they have different lengths, we can weigh them by their length.

to find the shortest path between a city A to a city B we can take the edges that creates a path between those two cities but take into account the edges with the lowest weights to find the shortest path between them.