# Read Assignment: Hash Tables

## Resources

Code Fellows [What Is A Hashtable](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-30/resources/Hashtables.html)

Paul Programming on YouTube [What Is A HashTable Data Structure](https://www.youtube.com/watch?v=MfhjkfocRR0&ab_channel=PaulProgramming)

HackerEarth.com [Basics of Hash Tables](https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/tutorial/)

Hash Table on [Wikipedia](https://en.wikipedia.org/wiki/Hash_table)

## Code Fellows Curriculum DSA Hashtables

Hash: Algorithm that takes an input and returns a value that can be used for security, or for an index into an array.

Buckets: Containers located at eash index of an array that store Values. This can be a 1:1 or 1:many relationship.

Collisions: More than key, when hashed, returns the same hash value.

Use Hash Tables to hold unique values, creating dictionaries, or developing a Library.

Each Node (or Bucket) is made up of a Key and Value pair.

Goal is to *quickly* store and find values by keys without having to search across many/all other items.

Searching an array is an O(n) read operation because worst-case scenario we would have to touch every item in the array.

Knowing exactly which index the value is at is a O(1) read operation because of N items in the array, only 1 is traversed/accessed.

A Hash Function is used to take an input, and guarantee the output is always the same, so it a good index-defining mechanism.

Using a Hash Function against and Array with n buckets (each containing zero to one value) is a O(1) read operation.

### Hash Functions

Turn a key into an integer: K => int

Hashtables are typically an Array of buckets of some large size (1024 is the author's favorite).

Suggested Hash Function Steps:

1. Add or multiply all ASCII values together.
1. Multiply the value by a prime number such as 599.
1. Use modulo to get the remainder of dividing value by the total size of the array.
1. Set or Get the value into the array and the resulting index.

Consider:

- Using multiplication over addition when hashing.
- Strings are just lists of Chars, so leverage char to get values to work with.
- Modulo somewhere near the end of the hashing function to get a reasonable index that will be within the backing Array size.

### Collisions

More than one key hashes to the same index in an array.

A perfect hash would never have collisions, and the worst possible hash always returns the exact same index into the array.

HashMaps need to be designed to handle collisions.

One way to work around collision issues is to modify the Array: Make each bucket a linked list, another array, or a BST.

When implementing buckets deeper than 1 level, store the index alongside the value in the bucket's Nodes.

### Set A Value

The curriculum author suggests this method to STORE a value in a hash map:

1. Accept a Key
1. Calculate the hash of the key
1. Use modulus to convert the hash into an array index
1. Store the key *with* the value by appending both to the end of the linked list

### Get A Value

The curriculum author suggests this method to RETREIVE a value from a hash map:

1. Accept a Key
1. Calculate the hash of the key
1. Use modulus to convert the hash into an array index
1. Use the array index to access the LinkedList representing the bucket
1. Search through the bucket looking for a node with the KVP matching the search term

### Load Factor

Tells us how full the hash table is.

To summarize Load Factor:

- Count of buckets with data divided by total number of buckets.
- As this approaches 1, the array is closer to "full" and there is increasing likelihood of collisions.

### Internal Methods

The curriculum author suggests these methods to use in hash tables.

#### Add()

1. Send the key to the GetHash method
1. Inspect the index location provided by GetHash method
1. If empty, add the KVP to the that index
1. If occupied, add the KVP to the data structure *within* that bucket

#### Find()

1. Send the key to the GetHash method
1. Inspect the index location provided by GetHash method
1. Await the return of the bucket's data structure to Search and return a value (or null)

#### Contains()

1. Accepts a Key
1. Call GetHash method on Key and return true if hash exists in the table, false otherwise

#### GetHash()

1. Accept a key as a string
1. Conduct hashing algorithm on the key
1. Return teh index of the array where the key/value should be placed

## Paul Programming Video Notes

Datastructure for storing information.

Utilizes Key Value pairs. Key is a sort of index, and a Value is the 'bucket' that stores the data associated with the key.

Make the initial hashtable storage size very large.

Hash Function: Takes a K, evaluates it to determine an indexing number, to determine:

- Where to store the Value initially.
- Where the value is stored if already there.

Hash Functions always return the same, predictable value given the same input.

Hash Collision: A hashed value returns an index where a value is already stored.

Ways to handle Collisions:

- Chaining: Turn the hash table bucket into a Linked List.
- Others (not discussed).

## HackerEarth Hash Tables Notes

## Anything From Wikipedia That Seems Useful

## Footer

Return to [Root README](../README.html)
