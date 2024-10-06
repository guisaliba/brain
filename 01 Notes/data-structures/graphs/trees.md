a tree is a data structure used to model connections between entities. each vertex is an entity and each connection is an edge, wher vertices are called **nodes** in any tree.

every tree is a graph but not every graph is a tree. to find out if a graph is a tree it has to attend some conditions:

1. a tree has n - 1 edges, where n is the number of nodes;
2. it has no cycles;
3. removing an edge from a graph and making it disconnected means it is a tree.
4. it has a root node (thus n - 1);

there is only and only one path from the root node to any other node, if there were to be more than one path, then it would be a cycle, meaning it is not a tree.

**leafs**, also called outer nodes, are nodes that do not connect any other node from them. **inner nodes** are quite the opposite, they make connections to other nodes.

any inner node is also the root of a subtree of the main tree, while a leaf can never be the root of a subtree.

every node, except for those that are leafs, are ancestors of other nodes (meaning they have parent nodes).

in a binary tree, all inner nodes have a degree of 3 and every node has both a left and right child unless they are leafs.