# Java IO Data and Object Streams

This page is a collection of notes taken while working through Oracle Java Tutorials and supplemental information made public by Baeldung.com.

## Oracle Java Tutorials Basic IO

### The Generic Interface Stream

Library: `java.util.stream`

Extends: `BaseStream<T,Stream<T>>`

"A sequence of elements supporting sequenctial and parallel aggregate operations."

Example aggregate operation using `Stream` and `IntStream` _[docs.oracle.com]_:

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

The end of a Stream Pipeline is denoted by a 'terminal operation', producing a result or _side effect_.

Streams are _lazy_, meaning they do not operate until the 'terminal operation' is initiated.

Source Elements are consumed on an as-needed basis.

Goals:

- Collections: Effeciently manage elements, and the access to them.
- Streams: Declaratively describe source, the computation operation for processing them in aggregate.
- BaseStream: This has `.iterator()` and `.spliterator()` methods to control Stream traversal, more like a collection.

Think of Stream Operations "as a query on the stream source." Could be similar to DotNET LINQ Operators.

Operations that alter the Source could cause unexpected Stream Pipeline behavior.

Use _lambda expressions_ `w -> w.getWeight()` to specify behavior.

Necessary behavioral parameters:

- Non-interfering: Behavior must not modify the source.
- Stateless: Results should not depend on any state that might change during execution.
- Non-null: Parameters _must not_ be null.

Streams Rules:

- Should only be operated upon _once_. Multiple traversals or forked streams are not allowed.
- Can throw `IllegalStateException` when Stream reuse is detected.
- Use `BaseStream.close()`: Streams with an IO-Channel source will require closing. Collection-sourced Streams do not. Use 'try-with-resources' to auto-close.

Streams can be made to be:

- Sequential: `BaseStream.sequential()` or `Collection.stream()`.
- Parallel: `BaseStream.parallel()` or `Collection.parallelStream()`.
- Query for seq/parallel: `BaseStream.isParallel()`.

Static Interface `Stream.Builder<T>` can be used as a mutable builder for a Stream.

### Byte Streams

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

_Always close streams_ - use a Finally block to safely close them:

```java
finally {
  // if a file was not opened, in will be null and never opened
  if (in != null) {
    in.close();
  }
  // same here, no file, out will be null and should not be closed
  if (out != null) {
    out.close();
  }
}
```

#### Summary of Byte Streams

- All other Streams are based on Byte Streams, but only use Byte Streams when it is appropriate for the data that is being manipulated.
- For example, when reading a text file, use Character Streams, not Byte Streams.
- Byte Streams are unbuffered.

### Character Streams

[Hava Basic IO Character Streams](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html).

- Store character values in Unicode.
- Transforms to 'local character set' e.g. 8-bit ASCII.
- Similar, no more complicated, than Byte Streams.
- Charcter Streams will auto-adapt to local character sets, supporting [internationalization](https://docs.oracle.com/javase/tutorial/i18n/index.html).
- Character Stream classes descend from `Reader` and `Writer`.

CopyCharacters class example _[Docs.Oracle.com]_:

```java
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class CopyCharacters {
  public static void main(String[] args) throws IOExecption {
    FileReader inputStream = null; // Character Stream uses FileReader for input
    FileWriter outputStream = null; // Character Stream uses FileWriter for output

    try {
      inputStream = new FileReader("input_file.txt");
      outputStream = new FileWriter("character_output_file.txt");
      int character; // holds Character VALUE
      while ((character = inputStream.read()) != -1) {
        outputStream.write(character);
      }
    } finally {
      if (inputStream != null) {
        inputStream.close();
      }
      if (outputStream != null) {
        outputStream.close();
      }
    }
  }
}
```

#### Bridge Streams

This sub-section is largely a copy from _[Docs.Oracle.com]_

- Use Bridge Streams to create Character Streams when no pre-packaged stream classes meet the need.
- Oracle has lessons in Sockets and Networking for creating character streams from byte streams provided by socket classes.

#### Line-Oriented IO

- Single Characters is not always the correct unit size.
- Ex: Line Terminators `\r\n` are multi-character encodings.
- Use `BufferedReader` and `PrintWriter` to support Line-Oriented IO (more on these later).
- These store and consume stream data in a `String` rather than an int, processing data line-by-line e.g. `.readLine()`.

_Note_: Line terminators _might be altered_ by PrintWriter from whatever the source terminator(s), to terminator(s) native to the current environment or Operating System.

Scanning and Formatting have more capability in regards to longer data read and write operations, and is covered in a later section.

### Buffered Streams

Unbuffered Streams:

- ByteStream
- CharacterStream
- Read and Write are handled directly by underlying OS.
- Blocking operations due to file-access locking semantics.

Buffered IO Streams:

- Read data from memory location instead of direct to/from hardware via OS.
- API provides access to memory 'buffer'.
- Use CTOR Wrapping to make an unbuffered stream use a Buffered API.

```java
var inputStream = new BufferedReader(new FileReader("input_file.txt"));
var outputSTream = new BufferedWriter(new FileWriter("output_file.txt"));
```

Four buffered stream classes:

- BufferedInputStream: Read ByteStreams.
- BufferedOutputStream: Write ByteStreams.
- BufferedReader: Read CharacterStreams.
- BufferedWriter: Write CharacterStreams.

#### Flushing Buffers

- Write-out buffered contents before the buffer gets full.
- Autoflush: Support provided by some output classes, happens during key events e.g. when `println` or `format` are called.
- Manually Flush a buffer by calling `flush()` method. Has no effect on unbuffered Stream types.

### Scanning and Formatting

Usually requires translating between human-friendly and computer-ready data strams.

- Scanner: Breaks input into 'tokens' (bits of data).
- Formatting API: Assembles data back to human-readable form.

#### Scanning

- Break down formatted input to a computer-ready data type.
- Default delimiter? White space characters (blank, tab, line terminators, etc see `Character.isWhitespace`).
- Use Delimiter method changes delimiter to a regex: `.useDelimiter(",\\s*");`

Scanner:

- Is _not_ a Stream class.
- Must be closed when done, just like a Stream class.
- Supports all primitive types _except char_.
- Support integer usage of the comma separater in US Locale, i.e.: `27,000` is an integer.

Basic Implementation of Scanner:

1. Initialize as null: `Scanner scanner = null`
1. Use `try-finally` block and ensure Scanner instance is closed before exiting the program.
1. Use `while (scanner.hasNext()))` to step through the delimited data tokens.

#### Formatting

PrintWriter (Character Stream class) and PrintStream (Byte Stream class) support formatting.

PrintWriter supports formatting an output stream for human use.

PrintStream is better for `System.out` and `System.err` data stream formatting.

Formatting Levels:

- `print` and `println`: Format individual values.
- `format` is similar to Format String and has many formatting options.

Use `System.out.format` with `%s` value placeholders, eol tokens, etc.

- `%`: Value placeholder.
- `s`: Conversion type String.
- `f`: Floating point.
- `n`: New line.
- `x`: Hexadecimal.
- `tB`: Integer to locale-specific month name.

_Note_: `%n` will always produce the correct New Line code for the local OS locale but `\n` will not!

Format Specifier Elements:

- Begin specifier with a `%`
- Argument index specifier: `1$` to identify specific argument to place, otherwise _in order left to right_
- Flags: `+0` formatting options such as preceeding '+' sign, the padding character e.g. '0', locale-specific thousands separator e.g. ',' _depends on selected conversion_
- Width: `20` minimum width of formatted value, _left padded_
- Precision: `.10` decimal places (for f) or total character length (for s), _right truncated_
- Conversion: `f` floating point

### IO From Command Line

Java handles this via 2 means:

- Standard Streams
- Console

Standard Streams:

- Read input from keyboard.
- Write output to the display.
- Support I/O on files and between programs, _up to the CLI interpreter not the application_.
- Are _Byte Streams_ not Character Streams.

Standard IOs are defined automatically in Java:

- System.in
- System.out (PrintStream)
- System.err (PrintStream)

To use Standard Input as a character stream wrap `System.in` in `InputStreamReader`.

### The Console

- Contains most features provided by Standard Streams.
- Useful for password entry, secure via `readPassword` method.
- Use its `reader` and `writer` methods to get input and output Character Streams from/to it.

There is a basic example of how to implement a [password changing program using the Conole](https://docs.oracle.com/javase/tutorial/essential/io/cl.html) by Oracle Docs.

### Data Streams

- Supports IO of primitive values.
- Supports IO of String Types.
- Implements either DataInput interface, or DataOutput interface.

Class DataOutputStream can only be instantiated as a wrapper to an existing ByteStream object, and provides buffers. Same for DataInputSTream.

```java
var out = new DataOutputStream(
  new BufferedOutputStream(
    new FileOutputStream(input_file)
  )
);
```

DataOutputStream methods include:

- `.writeDouble(double_value)`
- `.writeInt(int_value)`
- `.writeUTF(String_value)` -> Variable-width character encoding consumes a single byte for "common Western characters".

For both Input and Output the instantiation pattern is: File Stream(file_name), wrapped by Buffered Stream, wrapped by Data Stream.

_Note_: DataInputStream throws `EndOfFileException` when it finds the end of a file, rather than setting a specific state.

_Note_: Data Streams use Floating-point values to represent monetary Numbers, so certain decimals will not convert properly using Data Streams!

### Object Streams

- Supports IO of Object Types.
- Most standard classes support serialization, using interface `Serializable`.

Object Stream Classes are:

- ObjectInputStream
- ObjectOutputStream

Object Stream Classes implement subinterfaces ObjectInput and ObjectOutput of DataInput and DataOutput, respectively.

- All primitive data I/O methods supported by Data Streams are also supported in Object Streams.
- Object STream can contain mixture of primitive and object values.

Benefit: Object Streams support `BigDecimal` objects for fractional value representations (better than floating-point as in Data Streams).

#### Object Management Logic

Reconstituting an object from a stream can be tricky.

- References must be maintained, so they are traversed and added to the stream.
- Object Streams can only contain one copy of an object.
- Object Streams can contain _any number of references_ to the same object.
- The reconstituted duplicated object (by reference) will look like the same object when from the _same stream_.
- Referenced Objects within _multiple streams_ will look like individual objects to the consumer so _object References must be checked in addition to Equality_ at the consumer-side.

## Resources

[Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/essential/io/index.html).

Baeldung [Java Streams Links and Information](https://www.baeldung.com/java-streams).

Baeldung [Java IO Tutorials](https://www.baeldung.com/java-io) (mostly about file system manipulation).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
