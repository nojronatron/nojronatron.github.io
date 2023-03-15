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

## Byte Streams

8-bit data streams.

Byte Stream classes are decendants of InputStream and OutputStream.

Seems like its a good idea to import `java.io.IOException` for these streams.

Instantiate FileInputStream with the filename of the data source.

Instantiate FileOutputStream with a write-to filename.

```java
// always initialize Streams as null
FileInputStream in = null;
FileOutputStream out = null;

// set up the input and output files
in = new FileInputStream("input_file.txt");
out = new FileOutputStream("output_file.txt");
```

Use a loop to read-in data until FileInputStream sees byte `-1`.

```java
try {
  int character;
  while((character = in.read()) != -1) {
    out.write(character);
  }
}
```

*Always close streams* - use a Finally block to safely close them:

```java
finally {
  // if file was not opened, in will be null and never opened
  if (in != null) {
    in.close();
  }
  if (out != null) {
    out.close();
  }
}
```

### Summary of Byte Streams

All other Streams are based on Byte Streams, but only use Byte Streams when it is appropriate for the data that is being manipulated.

For example, when reading a text file, use Character Streams, not Byte Streams.

## Character Streams

I am [here](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html).

## Resources

[Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/essential/io/index.html).

Baeldung [Java Streams Links and Information](https://www.baeldung.com/java-streams).

Baeldung [Java IO Tutorials](https://www.baeldung.com/java-io) (mostly about file system manipulation).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
