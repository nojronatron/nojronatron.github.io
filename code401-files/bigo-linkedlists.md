# Big O and Linked Lists

## References

CodeFellows Common Curriculum Doc on [Big O Anlaysis of Algorithm Efficiency](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-05/resources/big_oh.html)

CodeFellows Common Curriculum Doc on [Linked Lists](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-05/resources/singly_linked_list.html)

What is a Linked List [Anyway part 1](https://medium.com/basecs/whats-a-linked-list-anyway-part-1-d8b7e6508b9d)

What is a Linked List [Anyway part 2](https://medium.com/basecs/whats-a-linked-list-anyway-part-2-131d96f71996)

## Big O Analysis of Algorithms

Running Time aka Time Efficiency aka Time Complexity:

"The amount of time a function needs to complete."

Memory Space aka Space Efficiency aka Space Complexity:

"The amount of memory resources a function uses to store data and instructions."

### Considerations

Evaluate Space and Time efficiency in terms of "worst case scenario"s.  
Key areas for analysis to consider:

- Input size: What the algorithm _reads_ including the _size_ of each parameter.
- Algorithm size in memory: How much space is needed to store the algorithm.
- Working/processing storage size: What memory is necessary to process in/out data within the algorithm.
- Output size: Storage needed to output the results of algorithm operating to completion.
- Units of Measurement: Milliseconds, Operations, and Basic Operations.
- Order of Growth: Running Time or Memory Space growth while algorithm executes. Constant? Logarithmic? Linear? Quadratic? Cubic? Exponential/Factorial?!?
- Best Case, Worst Case, and Average Case: Worst evaluates the worst possible input size of n; Best looks at best possible sizes of n; Average represents a typical or "random" input size of n.

Take a peek at this article at [InterviewCake.com regarding Big O Notation](https://www.interviewcake.com/article/java/big-o-notation-time-and-space-complexity)

### Asymptotic Notations

Big O: Worst Case scenario for an algorithm aka the upper bounds of Time and Space.

Big Omega: Best Case scenario for an algorithm aka the lower bounds of Time and Space.

Big Theta: Average Case scenario - tight bounds for Time and Space are considered.

## Linked Lists

- A sequence of Node objects.
- LinkedList is a Class that contains instantiated Nodes, as well as Properties HEAD and CURRENT.
- Nodes contain (at minimum): Some data property (state), and a REF to another Node (next).
- Connections between Nodes are made by reference.
- A Next (and/or previous) reference is used to traverse between Nodes (across a Linked List object).
- Singly-Linked Lists contain Nodes that _only know of their 'next' REF_.
- Double-Linked Lists contain Nodes that _know about their 'next' AND their 'previous' REF neighbors_.
- Circularly-Linked Lists have (at some point) a link that points _back to an existing Node_ in the same list.
- Do not use For loops! Use the Propeties Head, Current, and Next and a While condition to check for NULL or other value.
- A linear structure: Has a beginning, an end, and zero to infinite items in between without branches.
- Better use of memory allocation than an Array (it grows as needed).

### Keep These Top Of Mind

- Use pointers to track (and swap) references as needed while traversing, adding, removing, or otherwise interacting with a linked-list.
- For a circularly-linked list, the algorithm would need to take into consideration that a null might not ever be encountered.
- "A linked list is usually efficient when it comes to adding and removing most elements, but can be very slow to search and find a single element." _[Vaidehi Joshi, Medium.com, accessed 22-May-22]_

[Quoted in Medium.com](https://medium.com/basecs/whats-a-linked-list-anyway-part-2-131d96f71996)

### Considering Big O

Traversal:

- Time would be O(n) because it could take _traversing the entire list_ to find the value we are looking for.
- Space sould be O(1) because no additional space is needed other than the inputs for the list.

Adding a Node:

- Time would be O(1) as it is always inserted into the same place.
- Space is also O(1): No additional data or inputs are necessary to make the insertion.

## Footer

Return to [Parent Readme.md](../README.html)
