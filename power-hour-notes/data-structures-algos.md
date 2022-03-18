# Lets Get Physical With Data Structures And Algorithms

## Host

JB Tellez, long time developer (since Windows 95 days).

### Linked Lists

- Comprised of Nodes.
- Head is the 1st Node.
- Nodes contain values aka Data Properties.
- Nodes have a Next property that points to another Node or 'null'.

#### LL Depiction and How To Think About Them

Think of LL Nodes as playing cards, for example a 3-Node LL:

- All cards will have a Next with a value (reference) or null.
- One card will be Head, with a Next with value.
- The card in the Head Node's Next would be another Node.
- Another Node's Next would point to yet another Node.
- That third Node's Next value points to Null, making it the Tail Node.

#### How To Reverse a Linked List?

Could be an interview question!
Very difficult to do, strategies vary.
Easy to overthink the solution.

##### Strategies

Make a small change to the current state to get closer to the final state:

- Point Head Next to null.
- Point the other Links to their upstream sibling.

