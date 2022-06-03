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

Binary means 2, so Binary Tree Nodes are limited to K=2.  
Binary Trees allow insertions wherever a node will fit.  
Sorting is not a primary concern with Binary Trees.  

### K-ary Trees

K-ary Trees *can* have more tha 2 children per Node.  
Traversing is similar to Breadth First Traversal => Push Nodes into a queue but move DOWN the list of children of length k.  
*NO LONGER* checking for null at left and right children.  
Start from the Root and Enqueue it.  
Dequeue the Root and Enqueue it's Children.  

### K-ary Tree Code

BreadthFirst accepts a Root Node as input.  
A new Queue called Breadth is instantiated.  
Root is Enqueued to Breadth.  
Iterate so long as Breadth is NOT empty:  

1. Front is assigned the value of a Dequeued Breadth Node.
1. Front.value is returned.
1. An iterator Enqueues Front's Child Nodes into the Breadth Queue.
1. Rinse, Repeat through all Nodes.

## Adding a Node

Several Strategies, but basically there is not hard-and-fast rule about organizing or sorting while adding Nodes into a Binary Tree.  

One Strategy:

- Fill all CHILD Node spots from top-down utilizing Breadth-first Traversal.
- During BFTraversal find first Node that does NOT have all its Children and insert new Node there.
- Child slots are filled from Left-to-Right.  

To Specify a location where a Node should be placed:

1. Reference teh New Node to Create
1. Reference the Parent Node which the new Node will be Child to

### BigO Notation

Searching: O(n)  
Inserting: O(n)  

Breadth-First Traversal worst-case scenario will be O(w) where w=largest width of the Tree.  

### Perfect Binary Tree

Every non-Leaf Node has exactly 2 Child Nodes.  
Max-width for a perfect binary tree is 2^(h-1) where h=height.  
You can consider the height of the tree to be log(n) where n=number of Nodes.  

## The BST

A Binary Search Tree has structure attached to it.  
Organization is to place values smaller than Root to the left, and values larger than Root to the right.  

### Searching a BST

Pretty fast.  
Compare the Node you are searching for against Root.  
Value less than Root? Search Root.left.  
Value more than Root? Search Root.right.  

Utilize a While Loop to search a BST with the exit condition being a Leaf Node or the value Match.  

### BST BigO

Searching a BST is an O(h) operation where h=height or long(n) where n=number of nodes in BST.  
BST Insertion operations are same as Serach => O(h).  
An "unbalanced" BST search could be as bad as O(n).  
BigO Space Complexity of BST Search is O(1), because not additional space is allocated.  

## Footer

Return to [Root Readme](../README.md)
