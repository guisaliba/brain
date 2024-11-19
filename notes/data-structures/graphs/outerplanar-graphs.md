# Outerplanar Graphs

## 1. Outerplanar Graphs

### Definition
An **outerplanar graph** (also known as a **periplanar graph**) is a special class of **planar graphs** that can be drawn in the plane such that all vertices lie on the outer boundary (periphery) of the drawing, and no edges cross each other.

### Key Characteristics
- **Planarity:** Outerplanar graphs are inherently planar, meaning they can be drawn on the plane without any edge crossings.
- **Outer Boundary Embedding:** All vertices can be positioned on the outer face (boundary) of the planar embedding.
- **Forbidden Subgraphs:** Outerplanar graphs do not contain \( K_4 \) (the complete graph on four vertices) or \( K_{2,3} \) (the complete bipartite graph with partitions of 2 and 3 vertices) as subgraphs. These subgraphs are known to be non-outerplanar.

### Implicit Concepts Explained
- **Planar Graph:** A graph is **planar** if it can be embedded in the plane without any edges crossing. This means there exists at least one way to draw the graph on a flat surface such that its edges intersect only at their endpoints.
  
- **Subgraph:** A **subgraph** is a subset of a graph's vertices and edges that forms a graph. For example, \( K_4 \) is a subgraph consisting of four vertices with every pair connected by an edge.

### Examples of Outerplanar Graphs
- **Simple Cycles:** Any simple cycle, such as \( C_4 \) (a cycle with four vertices forming a square), is outerplanar. For instance, \( C_4 \) can be drawn with all four vertices on the outer boundary and edges forming the square without any crossings.
  
- **Trees:** All trees (connected acyclic graphs) are outerplanar because they can be drawn with all vertices on the outer boundary and no edge crossings.
  
- **Maximal Outerplanar Graphs (MOPs):** These are outerplanar graphs to which no additional edges can be added without losing outerplanarity. In MOPs, every face (including the outer face) is a triangle.

### Important Notes
- **Graph Representation:** A graph may have multiple planar embeddings. While one particular embedding might not appear outerplanar, if at least one embedding is outerplanar, the graph itself is classified as outerplanar.
  
- **Planarity vs. Outerplanarity:** Every outerplanar graph is planar, but not all planar graphs are outerplanar. For example, the complete graph \( K_4 \) is planar because it can be drawn without edge crossings, but it is not outerplanar. In any planar embedding of \( K_4 \), one vertex must lie inside the cycle formed by the other three vertices, violating the condition that all vertices must lie on the outer boundary.

## 2. Maximal Outerplanar Graphs (MOPs)

### Definition
A **Maximal Outerplanar Graph (MOP)** is an outerplanar graph to which no additional edges can be added without violating its outerplanarity. In other words, it is an outerplanar graph that is as edge-rich as possible.

### Characteristics of MOPs
- **Triangulation:** All internal faces (including the outer face) are triangles. This means every face is bounded by exactly three edges.
  
- **Edge Addition Constraint:** Adding any edge between two non-adjacent vertices in a MOP will result in a graph that is no longer outerplanar.

### Example
Consider a cycle \( C_4 \) representing a square. By adding one diagonal, the graph becomes a MOP because it is fully triangulated, and adding any more edges would require connecting vertices across the existing triangles, which would break outerplanarity.

## 3. Graph Thickness

### Definition
The **thickness** of a graph \( G \), denoted as \( \theta(G) \), is the minimum number of planar subgraphs into which the edges of \( G \) can be partitioned. Each planar subgraph in the partition must contain a subset of \( G \)'s edges such that:
- **Edge Coverage:** Every edge of \( G \) is included in at least one of the planar subgraphs.
- **Edge Exclusivity:** Each edge of \( G \) belongs to exactly one planar subgraph in the partition.

### Implications
- **Lower Thickness:** Graphs with lower thickness can be decomposed into fewer planar layers, making them simpler in terms of their planar representations.
  
- **Applications:** Thickness is relevant in areas such as network design, where minimizing the number of layers (to reduce complexity or cost) is desirable.

### Example
A planar graph has a thickness of 1 since it itself is planar. Non-planar graphs may have higher thickness values. For instance, the complete graph \( K_5 \) has a thickness of 2 because its edges can be partitioned into two planar subgraphs.
