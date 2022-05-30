# About Stacks and Queues

## Resource

Code Fellows documentation [Stacks and Queues](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/stacks_and_queues.html)  

## Stacks and Queues

Consist of Nodes that wrap data payloads, like Linked Lists.  
Common members: Push, Pop, Peek, and isEmpty.  
Common Concepts: FILO (First In Last Out) and FIFO (First In First Out).  

## Stacks

Use FIFO concept.  
First item PUSHed into the Stack is the first item POPped out of the Stack.  
Each Node's *next* property tracks the Node *below* it in the stack.  

```text
["charlie"]  <=  Top
    ||
  'next'
    ||
    \/
["bravo"]
    ||
  'next'
    ||
    \/
["alpha"]
    ||
  'next'
    ||
    \/
   NULL
```

### Operations Implmentations

#### PUSH

Push should always be an O(1) operation because the size of the stack does not affect the algorithm processing time.  
Push should assign "top" to the new Node, and assign the previous "top" to the new Node's "next" property.  
*Remember*: You must re-assign the "top" pointer to the new Node otherwise the Stack will not POP properly!  
*Optional*: The PUSH method could return a Boolean so the caller knows pass/fail of the operation.  
Another *option*: The PUSH method could *throw* a specific, documented exception if it fails otherwise return void, so the caller can make a valid assumption about pass/fail of the operation.  
Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*

```java
node = newNode(value)
node.next = top
top = newNode
```

#### POP

Pop removes the top Node from the Stack.  
Pointer 'top' should be re-assigned to the Node that is 2nd in line, prior to removing the current top Node.  
The Top Node (or its value) is returned to the caller.  
*Be sure to check isEmpty* property prior to POPping a Node from the Stack, to avoid raising an Exception.  
If you *are* going to raise an Exception, be sure details are passed-along to the caller and *document* the functionality so callers/users know they need to catch a thrown Exception.  
A 'temp' reference Node will need to be created to implement the 'Pop' functionality.  
The 'temp' reference Node will become the container that the method returns (probably temp.value in most cases).  
Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*  

```java
Node temp = top
top = top.next
temp.next = null
return temp.value
```

#### Peek

The Peek method is very simple and does not need to traverse the Stack at all.  
Simply return the top.value to the caller.  
Check 'isEmpty' prior to attempting to call top.next, and return something logical to the caller such as -1 or an appropriate Exception.  
Document the return types and exception type (if throws) so the caller knows how to manage pass/fail scenarios.  

## Queues

## Footer

Back to root [Readme](../README.md)
