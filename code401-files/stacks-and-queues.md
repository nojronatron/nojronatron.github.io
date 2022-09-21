# About Stacks and Queues

## Resource

Code Fellows documentation [Stacks and Queues](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/stacks_and_queues.html)  

## Stacks and Queues

Consist of Nodes that wrap data payloads, like Linked Lists.

Involved members: Push, Pop, Enqueue, Dequeue, Front, Rear, Peek, and isEmpty.

Common Concepts: FILO (First In Last Out) and FIFO (First In First Out).

When 'removing' a node i.e. POP or DEQUEUE, be sure to set all REFs on the removed Node to NULL so the garbage collector can clean up the unused reference types.

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

#### Stack Peek

The Peek method is very simple and does not need to traverse the Stack at all.

Simply return the top.value to the caller.

Check 'isEmpty' prior to attempting to call top.next, and return something logical to the caller such as -1 or an appropriate Exception.

Document the return types and exception type (if throws) so the caller knows how to manage pass/fail scenarios.

Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*

```java
// method throws an appropriate exception if Stack is empty
return top.value;
```

#### Stack isEmpty

Should return a boolean where "Is this Stack empty?" returns True if true, False if there are Nodes in the Stack.

An internal isEmpty Field *could* also exist, but is optional.

If an internal property is used then the 'isEmpty()' method could just be a protected getter/setter for the private property.

Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*

```java
return top = Null
```

The return resolves to a boolean result and is passed back to the calling method.  

## Queues

Queues are a FIFO data structure. LILO also works i.e. Last In Last Out.

Consider two ends of a pipe, and items are put in one end, and come back out the other end, in the exact same order.

Drawing a Stack as a left-to-right construct in a diagram might be helpful.

Left-to-right operations are:

```text
            'rear' vvvv                                'front' vvv
NULL <= next == ["charlie"] <= next == ["bravo"] <= next == ["alpha"]  <- 'dequeue' here
^
'enqueue' here
```

### Operation Implementations

#### Enqueue

Adding an item to a Queue is a O(1) operation because the new Node is always added in a single-shot operation to the 'rear' of the Queue.

It does not matter how many Nodes exist in the Queue a new Node is always inserted at 'rear' and 'rear' pointer gets moved to new Node.

The current 'rear' node.next property should point to the newNode, then the 'rear' pointer is reset to point to new Node.

Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*

```java
newNode = new Node(value)
rear.next = newNode
rear = newNode
```

#### Dequeue

Also an O(1) operation, as it does not matter how many Nodes are the Queue, it will be accomplished without any iterations or recursion.

Remove the Node that 'front' reference is pointing to and then return that Node or its value to the calling method.

*Remember* to replace the 'front' pointer reference to point to front.next prior to completing a Dequeue operation!

A temp Node will be required to hold the current 'front' node, move the reference to the front.next Node, and then return temp.value.

Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*

```java
Node temp = front
front = front.next
temp.next = null
return temp.value
```

#### Queue Peek

Also an O(1) operation, as it simply looks at, and returns, the front.value without tranversing the Queue.

Check isEmpty member prior to executing Peek method.

Alternatively, be sure an appropriate Exception is thrown if Peek tries to operate on an empty Queue.

*Always document* member operations including whether and when an Exception is thrown, and what TYPE of Exception will be thrown so the caller can handle these situations properly.

Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*

```java
return front.value
```

#### Queue IsEmpty

Returns a boolean value depending on whether Node count is 0 aka front is NULL.

This implementation relies on Enqueue() and Dequeue() methods to properly re/set front pointer to NULL when a Queue is emptied.

Recommended pseudocode, adapted from *[Code Fellows documentation, linked above]*

```java
return front = null
```

## JB Tellez on Stacks and Queues

JB came by class and reviewed Stacks and Queues for us.

### Overview

Execution or Call Stack: First In Last Out frames. It's a stack!

Getting back to something is pretty easy in a stack, compared to a willy-nilly random pile.

When the Call Stack is empty, the program is over / closed.

Queues are First In First Out: Formally ordered front to back.

With queues you put things in the front, and take things out of back aka end.

### Terminology

Stack

- Consisted of Nodes, similar to (or the same) as LinkedList Nodes.
- PUSH: Only puts things on TOP of the stack. Handles VALUES *only*!
- POP: Remove the last-in item from the "top" of the stack. *Could* throw an exception if stack is empty/null, but depends on the implementation.
- IsEmpty: Check the Stack if it is empty *before* trying to Pop it. Can use Try-Catch and handle any exception would be an implementation.
- Top: The top of the stack.  
- Peek: What's there at the top of the stack, without Popping it.

FILO

- First In Last Out
- Same a LIFO just flipped around
- The Top's Next is the Node that USED TO BE THE TOP

Pseudo Code for Push and Pop: See the DS&A Class-10 => resources => stacks_and_queues.md

*Important*: Be sure to update the this.top property with PUSH and POP operations:

- Top: private property that tracks the last-in Node reference, or null if there are no nodes
- Initial state of Stack: Empty list.head needs to be set to null
- Implement an isEmpty method to test the state of this.top and return true if null, false if has Node
- Push: Newly created node.next points to head, and then head is pointed to newly created Node
- Pop: head Node value is stored, then head pointer is moved to head.next, then value is returned to the user
- Implement a peek method to return the value of top only if isEmpty is false

Queue

- Queues have *two ends*: Front and Rear
- FIFO: First In First Out
- Enqueue: Nodes are items that are added to the *rear* of the queue
- Dequeue: Remove the FRONT Node from the QUEUE
- Front: Same as Rear when there is only one Node. Always the "next" node ready to be DEQUEUEd
- Rear: The last Node that was ENQUEUEd into the Queue
- Peek: Preview the value of the FRONT Node
- IsEmpty: Return True if QUEUE size is 0, False if > 0

The Next property of each Node points *toward the Rear* and *toward the Enqueue side* of the Queue.

Rear.next will always equal NULL.  

## Summary

Stack terminology: push, pop, top, peek, isEmpty.

Queue terminology: enqueue, dequeue, front, rear, peek, isEmpty.

Implementation Reminders:

- Exceptions or null or -1? Decide how your methods are going to return under certain situations like Peek when `isEmpty == true`
- Exception types: Be sure to select appropriate exception TYPE, or create and document a custom Exception to throw.
- If returning a value or a boolean for a negative situation, be sure it does not collide with an expected value i.e. integer type includes the value '-1' so that is not a good choice.
- Generics can be implemented and in fact ease some of the guesswork for true/false situations because this allows setting 'null' values which are slightly easier to test for than primatives.
- Utilize a TEMP node when POPping or DEQUEUEing so the top or front reference can be moved and value can be returned.
- Create a new Node to store a value when PUSHing or ENQUEUEing so the calling method doesn't need to understand the Node class.
- Use O(1) algorithms to perform all actions to keep Stack and Queue simple and linear in space in time computationally.

## Footer

Back to root [Readme](../README.md)
