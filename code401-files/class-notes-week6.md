# Class Notes Taken During Week 6 Java 401

## Monday 20 June

Class canceled.

### Lab Class 26

Wants Style, Color, and Fonts.

See paper notepad for list of Font and Color pallette options.

## Summer Solstice

Class will be held, run by David Souther.

### Data Structures

Arrays, LinkedLists, Stacks, Queues, and Trees.

Use Linked Lists when editing data mostly near the end of a list.

Use a Tree when you want to keep things sorted => They will make it faster to locate data or determine if the tree contains the data at all.

#### Maps

They are KVPs.

The notion of a map is tied to Keys (things to consider when going into the map to find values) and Values (the value).

Bracket notation and dot-notation are examples of KVPs.

ArrayLists: Index is the key; Value at that index location is the... value.

Array constraints: Indexes will be zero-based and less than the total length of the array values count.

For Maps, we want to find the value quickly.

TreeMap: Maintains a backing "Tree" to help find data.

Invariance: "The rules" under which a datastructure operations.

Map Invariant Rules:

- Keys are unique
- Keys have meaning (not random)

TreeMap Invariants:

- Keys must be sortable (have an ordering)
- O(log(n)) algorithmic time

*Note*: TreeMaps can be slow unless the data is unsorted, and HashMaps are more common.

Hash Invariants:

- Uses a hash to calculate indices of the data.
- Uses an Array that *holds* the data.
- Arrays are fixed size
- Keys could be *infinite*


## Footer

Return to [root readme](../README.html)
