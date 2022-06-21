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

Uniquely ID's an object from a group of objects.

- Students assigned a unique ID, used to retrieve data about them.
- Books assigned a unique number, used to find location of book in the library, if the book is checked out, etc.

Use a hashing algorithm to define and utilize keys that are large or complex.

Ideal Hash Tables will store data within their structure evenly/smoothly.

Recommended 2-step Hashing:

1. Convert element into an int with a hash function.
1. Store the element int othe hash table for quick retreival using the result of int modulo size_of_array.

Suggested hashing algorithm:

```sh
hash = hashfunc(key)
index = hash % array_size
```

### Hash Functions Should Be

1. Easy to compute: Must not become an algorithm itself.
1. Uniformly distribute data into a structure: Should not result in clustering.
1. Fewest Possible Collisions: Avoid collisions to avoid increasing bucket sizes thereby reducing speed of the hash table processing.

### Hash Function Should Do's

Use Prime Numbers in the calculation, like '599', to reduce the probability of collisions.

Use key * prime modulu size_of_array to further segregate similar data.

The larger the backing storage structure, the better the modulus will do at returning an empty index.

### Hash Table

Stores KVPs.

Leverages a Hash Function to find values based on keys, and find locations to store KVPs.

The *average* time required to search for an element in a reasonably well designed hash table is O(1).

### Collision Resolution Techniques

#### Separate Chaining / Open Chaining

Commonly used.

Uses Linked Lists.

Each bucket *is* a Linked List if it contains data at all.

KVP's with same hash-function output values (hash codes) get stored, in-order, within the Linked List bucket.

Worst-case scenario is when all entries are inserted into the same linked list.

#### Linear Probing / Open Addressing / Closed Hashing

All entry records are stored in the array itself.

When a collision occurs, a *Probe Sequence* is followed until the an empty index is located.

Probe Sequence:

- Followed while traversing through entries in collision avoidance routine.
- Alters intervals between successive entry slots in the probes.
- An empty index indicates an unused slot that can then be used.

Linear Probing: Use a fixed count to traverse beyond any collided slot.

Linear Probing Algorithm example:

```sh
index = index % hash_table_size     # 1st try collides
index = (index + 1) % hash_table_size # might also collide so
index = (index + 1) % hash_table_size # ...etc
```

*Jon Note*: This technique could also force your Search and Get methods to run additional code in order to find the stored value.

#### Quadratic Probing

Similar to Linear Probing but interval is increased dramatically between collision detected slots.

```sh
index = index % hash_table_size             # collision
index = (index + pow(1, 2) % hash_table_size) # might also collide
index = (index + pow(2, 2) % hash_table_size) # etc
```

When using Quadratic Probing you must be certain the underlying array size is large enough that the hashing algorithm will likely find an open spot.

*Jon Note*: This technique could also force your Search and Get methods to run additional code in order to find the stored value.

### Double Hashing

Similar to Linear Probing but the interval between successive probes is computing using a second hash function.

Example probing sequence pseducode:

```sh
index = ((index + 1) * indexH) % hash_table_size # might collide
index = ((index + 2) * indexH) % hash_table_size # etc
```

*Jon Note*: This technique could also force your Search and Get methods to run additional code in order to find the stored value.

### Applications for Hash Tables

- Implement associative arrays, where indices are arbitrary strings or complicated objects.
- Database indexing.
- Caching data in front of a DB or other service where data I/O is slower than in memory.
- Representing objects e.g. languages like Perl, Pythin, JS, and Ruby, etc.
- Sets: Storing *only* unique values into table(s).
- Transposition Table: Complex hash table stores info about data table sections that have been searched *[Wikipedia]*.

## Anything From Wikipedia That Seems Useful

There are multiple re-hashing techniques that can be utilized to resize an existing hash table.

Some re-hashing methods perform the re-hasing session against the entire table, others do so proportionally and during usual operation.

One method that could be implemented is to have an old-new-hashcode algorithm where a new hashing algorithm is implemented and the add and search functions that call data after table is incrementally increased use the newer algorithm, but the data blocks not yet touched do not.

## Footer

Return to [Root README](../README.html)
