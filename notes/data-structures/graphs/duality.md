# Duality in Graphs

### Definition
**Duality** refers to a relationship between two planar graphs, where one graph is the **dual** of the other. For a given planar graph $G$, its dual graph $G^*$ is constructed based on the embedding of $G$ in the plane.

### Construction of Dual Graph $G^*$
- **Vertices of $G^*$ :** Each face (including the outer face) of $G$ corresponds to a vertex in $G*$.
  
- **Edges of $G^*$:** For every pair of adjacent faces in $G$, there is an edge between the corresponding vertices in $G^*$. Specifically, if two faces in $G$ share a common edge, the dual graph $G^*$ will have an edge connecting their corresponding dual vertices.

### Properties
- **Planarity Preservation:** If $G$ is a planar graph, so is its dual $G*$.
  
- **Double Dual:** The dual of the dual graph $G^*$ is isomorphic to the original graph $G$ , assuming $G$ is connected.
  
- **Adjacency Preservation:** Adjacency of faces in  $G$ translates to adjacency of vertices in $G^*$.

### Example
Consider a planar graph $G$ shaped like a triangle (a $C_3$ cycle). Its dual$G^*$) will also be a triangle since there are three faces (including the outer face), each adjacent to the other two.

### Important Considerations
- **Planar Embedding Dependency:** The dual graph depends on the specific planar embedding of $G$. Different embeddings of the same graph $G$ can lead to different dual graphs.
  
- **Non-Planar Graphs:** Duality is only defined for planar graphs. Non-planar graphs do not have duals in the traditional sense.