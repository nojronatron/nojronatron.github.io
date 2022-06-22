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
- Arrays are fixed size.
- Keys could be *infinite*.
- Needs to take a key, turn it into an index to store in the array.

Hash Functions

- Uses a calculation to determine index of value that is being searched
- Transforming/converting types to make them calculable
- Should be an O(1) search function
- Hash takes O(k) => depends on the key length

Hash Collision

- Multiple keys map to the same index
- Pidgeonholing: 4 pidgeons, 3 coupes => will multiple pidgeons be in a single coup? Yes. If n > k then at least 1 k will have n > 1 items in it.
- To avoid this use an Array, Linked List, or Balanced Tree to add data instances to the index.
- Resizing is an option, but "book keeping" under the covers is a somewhat expensive operation.

Hash Index Implementations

- There could be several.
- One implementation has the constraint of "the key MUST have a hashCode() method" - thankfully Java's Object allows .getHash() is inherited to all children.

What Is A "Good Hash Code"?

- Meets constraints and doesn't break assumptions.
- Statistically guarantee that the index values will be unique.
- Use prime numbers to return the hash.
- Use a power-of-2 size array to store the data.

Scaling:

- Ensure the total number of 'buckets' is a prime number (or a power of 2).
- Multiply the hash value by a large prime number to consume the entire index space that is avaialble.

Where would HashMaps be implemented?

- Proxy or cache for a slower file system: Use filename as key.
- Discover basketball player's score statistics.

When should I think about using a Map?

- When the keys in a KVP are strings instead of numbers.
- When using data structures that are not a tree or some sort of in/out stack or queue.
- When interacting with, storing, and querying unstructured data.

Random Accessing map items (for add or update):

- `int value = map.contains(key) ? map.get(key) : default_value;`
- contains method could be different syntax.

Assignment:

- Implement a hashtable
- Implement the basic API functions (get, set, contains, keys, and hash)
- Collisions must be handled in get and set (could be sloppy or nice e.g. rehashing etc)
- Optionally: Track size of the hashtable
- Returning collection of keys will require some tips/hints searching
- Optionally: Create an interface to force implementation
- Single Responsibility
- Write Tests
- Document
- Catch errors

### Key Takeaways

Big-O Analysis is not the be-all, end-all:

- Memory is limited, but you can always buy more.
- Memory fragmentation in large data sets will cast lots of processing time (large linked lists).
- Processing time is essentially linear (it's not 1987 anymore -David Souther).

Dealing with Data Structures you *must consdier bit/byte sizes of the data*:

- CharCode is an int
- Primative int is 4 bytes aka 32 bits
- ASCII char codes are 7 bits

Pigeonholing Algo:

- Ceiling(n/b) aka round-up result of (num_pigeons / num_coops)

## Weds Class Notes

### Android Development Overview

- Android Studio (IntelliJ for Android dev)
- WYSIWIG editor built-in

Bring-forward learnings from Code 301 e.g. React and Components.

### Intro To Android Studio

We are going to build "Task Master" project that will build upon for the remainder of this course.

Do lots of exercising with UI Constraints to experience how they impact the UI in the emulator.

There will be times you will need to CLI-kill the emulator: Find PID, use kill command. Emulator has the PID.

Event Listeners: `onClick()` etc. They do not handle everything for you, but will be used a lot for Android development.

Vocabulary:

- Emulator: Virtual device, not a replacement for a physical device but is a handy stand-in.
- Activities: Analogous to an MVC View.
- MPA/SPA: Multi-page Application (Thymeleaf/MVC) and Single-page Application (React).
- Fragments: SPA uses these reusable blocks of code to dynamically render a page to a single Activity.
- Intents: Routes Between Activities.
- Extra: Another thing related to Intents that we might not work with.
- Component Tree: 
- Espresso: Integration Testing.

Today:

- Add 3 Activities.
- Homepage: Match the wireframe. Color scheme and exact layout is up to you but simply get this 1st round to look like the Lab.
- Add a Task: 2 inputs and 1 button. NO DATA PROCESSING, just UI and Event Handlers.
- All Tasks: ??
- Stretch Goal: Style the app!
- MUST build an APK and TEST IT (emulator to install and open).

### A Look Ahead

Week 1: Android basics.

Week 2: AWS Amplify, then try push to GooglePlay Store.

Week 3: File Storage, Location, and Mine? AWS? Launching other Apps from out App.

Week 4: Analytics and Lectures, as well as monetization of mobile apps, as well as OSS contributing.

Week 5: Final Presentations Week!

About 3 to 7 AWS technologies will be discussed throughout.

Consider getting AWS Certificates post-Code 401, but don't forget having completed school work to *prove* your knowledge.

Consider MOB PROGRAMMING and DEBUGGING to help get through various blockers/issues throughout these weeks.

### Hash Maps

Sets and Maps are like really big arrays.

Hash Maps are in best-case O(1), and lookup based on keys is very effecient even with very large data sets.

Do *not* just overwrite data, use collision handling (chaining etc) to deal with duplicate keys.

Handling collisions will be a *requirement* going forward.

## Footer

Return to [root readme](../README.html)
