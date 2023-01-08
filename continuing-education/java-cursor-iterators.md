# Java Cursor and Iterators

Iterators are functions that can loop through a collection of some type.

A cursor is a placeholder that always lies *between* items in a collection of some type.

## Cursor

The Cursor concept is exposed via `java.util Interface Iterator<E>`.

The interface is found within the [Java Collections Framework](https://docs.oracle.com/javase/7/docs/technotes/guides/collections/index.html).

E => The type of elements returned by this iterator.

A collection with n elements has n+1 cursor positions.

Cursor can return:

- The item in the position directly preceeding it.
- The *index* of the position directly preceeding the cursor position.
- The item in teh position directly following it.
- The *index* of the position directly following the cursor position.
- Boolean whether there is a *next* following the cursor position (therefore might have a value).
- Boolean whether there is a *previous* preceeding the cursor position (same).

Cursor can also:

- Remove the last returned item from the collection.
- Set/replace the last item returned from the collection.

*Bottom Line*: Consider the cursor an ephemeral pointer used to placehold *between* elements of a collection, and as a demarcating tool when it is at the beginning (-1) or the end (length) of a collection.

The following Iterfaces utilize Cursor to perform naviation and operations on collections.

## Interface List Iterator<E\>

List Iterator makes use of Cursor to navigate, insert into, and remove from, the collection.

It's Superinterface is `Iterator<E>` (detailed below).

Methods:

- hasNext(): Returns Boolean.
- next(): Returns Element. Throws NoSuchElementException.
- hasPrevious(): Returns Boolean.
- previous(): Returns Element. Throws NoSuchElementException.
- nextIndex(): Returns int. Note: Returns list size if at end of list.
- previousIndex(): Returns int. Note: Returns -1 if at beginning of list.
- remove(): Returns void. Removes last element returned by next() or previous(). See details below.
- set(optional E): Returns void. Replaces last element returned by next() or previous(). See details below.
- add(optional E): Returns void. Inserts specified element into the collection. See details below.

### Remove, Set, and Add

Restrictions on using remove():

- Can only be called once per next() or previous() call.
- Cannot be called after add(E).

Restricutions on using set(E):

- Cannot be called after remove() nor add().
- next() or previous() *must* have been called just prior to.

Restrictions on using add(E):

- *Inserts* into the element space immediately *before* the element that next() would return.
- The inserted element is also immediately *following* the element that previous() would return.
- *Both* previous() and next() indices are incremented by 1 (this is because `cursor` is *between* previous() and next()).

remove() Throws:

- UnsupportedOperationException: Not supported by this list iterator.
- IllegalStateException: Neither next() nor previous() have been called prior to remove().

set() Throws:

- UnsupportedOperationException.
- ClassCastException: The element class is not compatible with the Iterator Element Type declaration.
- IllegalArguementException: Element cannot otherwise be added to the list.
- IllegalStateException.

add() Throws:

- UnsupportedOperationException.
- ClassCastException.
- IllegalArgumentException.

## Interface Iterator<E\>

E: The type of element returned by the iterator.

This is a parent interface to subinterface `ListIterator<E>`.

`Scanner` class implements this interface.

Iterator is a forward-navigating interface. ListIterator has additional functionality based on this one.

### Methods

hasNext(): Returns boolean.

next(): Returns next Element in the iteration. Throws NoSuchElementException.

remove(): Returns Element on a conditional basis (see below). Throws (see below).

Conditions of remove():

- `next()` *must* have been called prior to calling remove().
- The element returned by the last `next()` call is removed from the collection.
- Can only be called *once* per call to `next()`.
- Is not synchronized for parallel operation.

remove() throws:

- UnsupportedOperationException: Operation not supported by this iterator.
- IllegalStateException: If `next()` has not been called, or `remove()` has already been called since the last `next()` call.

## Difference Between Iterator and Enumeration

### Enumeration<E\>

Enumerations are used to retrieve elements from a collection or specify input streams to SequenceInputStream.

Create an enumeration on a collection by calling `elements()` on it.

Utilize method `nextElement()` to move the enumeration pointer forward through the collection once per call.

```java
Enumeration<String> enumeration = myCollection.elements();
while(enumeration.hasMoreElements()) {
  // do stuff
  enumeration.nextElement();
}
```

### Iterator<E\>

Iterators enable retrieving elements one-by-one.

Read and Remove operations are supported.

Are universal and can be applied to all collections.

Create one by calling `iterator()` method in any collection.

```java
// create a myList collection and then...
Iterator<String> itML = myList.iterator();

while (itML.hasNext()) {
  // iterate using next
  if (itML.next() == 'some value') {
    // remove the current element
    itML.remove();
  }
}
```

ListIterator<E\> allows iterating in both directions (forward and backward) as explained earlier in this document.

## References

Oracle Docs [java.util Interface ListIterator](https://docs.oracle.com/javase/7/docs/api/java/util/ListIterator.html).

Oracle Docs [java.util Iterator<E\>](https://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html).

Oracle Docs [Java Collections Framework](https://docs.oracle.com/javase/7/docs/technotes/guides/collections/index.html).

Baeldung blog post on [Iterator and Enumerator](https://abhimanyu081.medium.com/three-cursors-in-java-collections-c93f75f69b16).

## Footer

Back to [ContEd Index](./conted-index.html)

Back to [Root README](../README.html)
