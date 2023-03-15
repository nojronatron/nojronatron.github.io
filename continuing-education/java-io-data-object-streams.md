# Java IO Data and Object Streams

This page is a collection of notes taken while working through Oracle Java Tutorials and supplemental information made public by Baeldung.com.

## Oracle Java Tutorials Basic IO

## The Generic Interface Stream

Library: `java.util.stream`

Extends: `BaseStream<T,Stream<T>>`

"A sequence of elements supporting sequenctial and parallel aggregate operations."

Example aggregate operation using `Stream` and `IntStream` *[docs.oracle.com]*:

```java
int sum = widgets.stream()
  .filter(w -> w.getColor() == RED)
  .mapToInt(w -> w.getWeight())
  .sum();
```

`IntStream` is one of several 'primitive specializations' (Streams).

A Stream represents a pipeline.

Stream Pipeline sources could be Collections, Arrays, a Generator Function, I-O Channel, etc.

Stream Pipelines include a processing section for 'intermediate operations'.

The end of a Stream Pipeline is denoted by a 'terminal operation', producing a result or *side effect*.

Streams are *lazy*, meaning they do not operate until the 'terminal operation' is initiated.

Source Elements are consumed on an as-needed basis.

Goals:

- Collections: Effeciently manage elements, and the access to them.
- Streams: Declaratively describe source, the computation operation for processing them in aggregate.
- BaseStream: This has `.iterator()` and `.spliterator()` methods to control Stream traversal, more like a collection.

Think of Stream Operations "as a query on the stream source." Could be similar to DotNET LINQ Operators.

Operations that alter the Source could cause unexpected Stream Pipeline behavior.

Use *lambda expressions* `w -> w.getWeight()` to specify behavior.

Necessary behavioral parameters:

- Non-interfering: Behavior must not modify the source.
- Stateless: Results should not depend on any state that might change during execution.
- Non-null: Parameters *must not* be null.

Streams Rules:

- Should only be operated upon *once*. Multiple traversals or forked streams are not allowed.
- Can throw `IllegalStateException` when Stream reuse is detected.
- Use `BaseStream.close()`: Streams with an IO-Channel source will require closing. Collection-sourced Streams do not. Use 'try-with-resources' to auto-close.

Streams can be made to be:

- Sequential: `BaseStream.sequential()` or `Collection.stream()`.
- Parallel: `BaseStream.parallel()` or `Collection.parallelStream()`.
- Query for seq/parallel: `BaseStream.isParallel()`.

Static Interface `Stream.Builder<T>` can be used as a mutable builder for a Stream.

## Resources

[Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/essential/io/index.html).

Baeldung [Java Streams Links and Information](https://www.baeldung.com/java-streams).

Baeldung [Java IO Tutorials](https://www.baeldung.com/java-io) (mostly about file system manipulation).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
