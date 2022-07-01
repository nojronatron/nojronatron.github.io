# Read About Implementing Graphs

## References

Code Fellows Curriculum: [Graphs](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/graphs.html)

## Terminology

Graphs ar non-linear data structures.

Consider them a collection of vertices (nodes).

Nodes are connected by line segments (Edges).

A Neighbor is a directly adjacent Node to another Node, connected by an edge.

A Degree is the count of edges connected to that Node.

Vertices (Nodes) are often labelled with single-character letters like 'a', 'b', and so on.

Edges are indicated using a bracketed enclosure with pairs of Nodes e.g. `{ (a,c), (b,c), (b,f), (c,e)...}` etc.

## Directed and Undirected

Undirected: A graph where each edge is bi-directional.

When drawn, there ar eno arrows between Nodes, meaning no specific path must be followed to reach any other Node along any Edge.

Directed: Every edge is directed, meaning arrow of direction are indicated.

AKA Digraph.

Each Node is directed at another Node, like a reference to 'Next Node'.

## Complete, Connected, and Disconnected

Complete: All Nodes are onnected to all other Nodes once.

Connected: All Nodes have *at least* one edge. A 'Tree' is a form of Connected Graph.

Disconnected: Some Nodes may not have edges. Stand-alone Nodes could be described as Disconnected Graphs or 'Islands'.

## Acyclic and Cyclic Graphs

Acyclic:

- Directed Graph without cycles.
- Cycles are defined by loops within a graph where a path from one Node could *potentially* lead back to itself.
- Directed Acyclic Graph "DAG": Acyclic Graph with Directed edges. Trees can be thought of as DAGs.

Cyclic:

- A Graph that has cycles.
- A path that starts and ends at the same Node.

## Graph Representation

Depictions of graphs are usually done through Adjacenty Matrix, or Adjacency List.

Adjacency Matrix:

- If there are n Vertices, then there are n x n Nodes in the Matrix.
- Vertices are represented by each row and column.
- In a Boolean Adjacency Matrix, rows and columns are only connected where the vertices' crossings add up to one.
- An undirected graph is always symmetric.
- Directed graphs will not always be symmetric.

## Sparse and Dense Graphs

Sparse: Few connections within the Graph.

Dense: Many connections within the Graph.

## Adjacency List

The most common way to represent graphs.

A collection of linked lists or arrays of lists.

Easy to view if one vertices connects to another.

Where there is no connection between vertices, they are not listed.

Items of Note:

- Adjacency Lists are Collections.
- Nodes represented in a graph through lists of verices (Linked List or List in an Array) show intersections.
- Whenever a Edge is discovered, add it to the correct vertices in the List.

## Weighted Graphs

Numbers mark each of its edges: Weights.

Set elements in the 2D array to represent actual weight between 2 paths.

No connection? Weight = 0 (or infinity).

A weighted matrix can be represented in a L x W Graph Representation, or an Adjacency List (Array with buckets).

In an Adjacency List, the Weighted Matrix Nodes and Values are stored in the vertices e.g. `d => a,0 => b,5 => c,6`

## Traversals

### Breadth First

Start at a specific Vertex/Node, specifying it when calling the Breadth First function.

Graphs can have cycles, but otherwise look and act a lot like Trees.

Add a tracking mechanism to the code (e.g. a Queue or Stack?) to avoid revisiting already-visited Nodes.

Algorithm Pseudocode:

```sh
Enqueue the root node.
Iterate while the Queue is not empty.
Dequeue the 1st Node.
Add unvisited child Nodes to the Queue.
```

More Specific Pseudocode:

```sh
ALGORITHM BreadthFirst(vertex)
  DECLARE nodes INSTANTIATE new List
  DECLARE breadth INSTANTIATE new Queue
  DECLARE visited INSTANTIATE new Set

  breadth.Enqueue(vertex)
  visited.Add(vertex)

  while (breadth is not empty)
    DECLARE front and assign value of breadth.Dequeue
    nodes.Add(front)

    for each child in front.Children
      if (child not inside visited set)
        visited.Add(child)
        breadth.Enqueue(child)

  return nodes
```

Notes about Breadth First usage in Graphs:

- Disconnected Nodes will not be visited.
- Island Graphs will not be visited nor returned by the algorithm.

### Depth First

Use a Stack to visit children of a subtree.

*Note*: Traversing Trees Depth First leverages the Call Stack, here a separate Stack object will be instantiated.

Algorithm:

- Add root Node to the stack.
- Mark the root Node as Visited.
- Pop a Node off the stack and check its neighbors.
  - If a neighbor has not been visited push it onto the Stack and mark it as Visited.
  - If a neighboar HAS been visited just ignore it.
- Repeat for other neighbors.
- Once the stack is empty, return Visited to the caller.

## Real World Usages

- GPS
- Mapping
- Driving Directions
- Airline Traffic Control
- Product Suggestion Algorithms

## TODOs

- [ ] review graphs
- [ ] translate pseudocode into real code
- [ ] execute tests and debug step-throughs to see them in-action
- [ ] research other uses for graphs

## Footer

Return to [Root README](../README.html)
