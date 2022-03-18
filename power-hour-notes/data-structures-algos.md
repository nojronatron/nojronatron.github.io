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
- Always hand-off the links between nodes so that Head always has a reference to a Next???
- The last Node move is to move Head to Previous.
- The 'stop' signal is when Current Node is null.
- The final step is to set Previous Node and Temp Node references to null (cleanup).

*Advice*: Ed Y. recommends running the process forward AND backwards to ensure the original list is the final result.

Strictly: You can only reference Nodes while Current.Next is not null.

1. Set Upcoming Node to Head.Next.
2. Set Head.Next to null.
3. Set Previous to Head.
4. Set Current to Upcomming.
5. Set Upcoming to Current.Next.
6. Set Previous to Current, Current to Upcoming, to Upcoming.Next.
7. Continue until Current Node is null.  

## Resources

From Ed Y.: Relevant Video on [YouTube](https://www.youtube.com/watch?v=LH5ay10RTGY)  
From Ed Y.: Linux Kernel - Better Way(s) to iterate through a Linked List [LWN.net](https://lwn.net/SubscriberLink/887097/7ca69c6bfa3584c0/)