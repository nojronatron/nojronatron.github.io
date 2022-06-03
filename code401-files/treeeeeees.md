# Read About Trees

## Resources and References

From [Code Fellows Common Curriculum DS&A Trees](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-15/resources/Trees.html)  

## So Many Trees

Trees are made up of Nodes that have a value and references to at least one other Node and possibly Null.

Node Types include:

- Root: The beginning Node of a tree.
- Left: Reference to child Node on the current Node's "Left" side.  
- Right: Ref to "Right" child Node.
- Edge: Link (reference) between child and parent Nodes.  
- Leaf: Node without Children.

Other common Tree Properties:

- K: The max number of Children any single Node can have.
- Height: The height of a tree equals the number of edges from the Root to the furthest Leaf.

## Traversals

Primary Traversal Types are Depth First and Breadth First.

Multiple methods of *Depth First* traversals can be done:

- Pre-order: root, then left, then right
- In-order: left, then root, then right
- Post-order: left, then right, then root

*Important*: Pay attention to what is happening to the Root Node in these Depth First traversals.  

### Preorder Code

Preorder accepts a Root Node (the starting position).  
Test: root.left is NOT null then recurse and supply root.left as argument.  
Test: root.right is NOT null then recurse and supply root.right as argument.  
Returns: root.value.  

### Recusive Functions

Each iteration through recursive calls places the current method execution into the Stack.  
Stacked Functions are executed *without removing the previous execution*.  
Reaching a Leaf Node is equivalent to finding a Null on a Node.left or Node.right reference.  
Finding Null is a valid way to "exit" a recusive functions' current execution run.  

*Remember*: When a function exits and "pops off the Stack" the return value becomes available *at that time*.  

When the "top" recursive function call returns, the previous (new "top") continues executing where it left off.  

### Inorder Code

Inorder accepts a Root Node.  
If Root Left is NOT null, recursively call Inorder and supply root.left as the argument.  
Return root.value.  
If Root Right is NOT null, recursively call Inorder and supply root.right as the argument.  

### Postorder Code

Postorder accepts a Root Node.  
If Root Left is NOT null, recursively call Postorder and supply Root.left as the argument.  
If Root Right is NOT null, recursively call Postorder and supply Root.right as the argument.  
Return root.value.  

### Breadth First

Iteration occurs *at each lateral level* of the Tree, from left-to-right, then top-to-bottom.  
Breadth First Trees use a Queue to track the traversal.  
Every time a Node is walked (traversed) it is placed into a Queue.  
Every time there is at least one Node in the queue, it is Dequeued and it's CHILDREN are Enqueued, left, then right.  
Rinse, repeat.  

### Breadth First Code With Builtin Queue

BreadthFirst accepts a Root Node.  
A Queue named Breadth is instantiated.  
An iteration is entered until Breadth is emptied:

1. node front is assigned breadth.dequeue
1. front.value is returned to the calling method
1. if front Left is NOT null enqueue front.left
1. if front.right is NOT null enqueue front.right

## Binary vs K-ary Trees



## Footer

Return to [Root Readme](../README.md)
