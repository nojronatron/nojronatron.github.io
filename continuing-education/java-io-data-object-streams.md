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

[Java Basic IO Character Streams](https://docs.oracle.com/javase/tutorial/essential/io/charstreams.html).

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
- Supports all primitive types _except_ 'char'.
- Support integer usage of the comma seperator in US Locale, i.e.: `27,000` is an integer.

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

### File IO with NIO.2

Oracle Java Docs refers to JDK 8 release and java.nio.file package and its sub-packages in this sub-section.

The documentation reviews paths, both relative and absolute, and Symbolic Links.

Unix-based paths are not comparable to Windows-based paths due to their native naming convention. However, both can be handled and processed by Java.

Symbolic Links are:

- Symlinks.
- Soft links.
- Special file that serves as reference to another file.
- Abstact-away the sideways traversal to another Path.
- Automatic redirectors to the actual referenced file, aka the Link Target.
- Transparent to the OS user.
- Exceptions are thrown when a symbolic link no longer exists (deleted, renamed, mis-spelled, etc).
- Capable of circularly-referencing.

Java handles circularly-referenced Symlinks.

#### Paths

Create a path using the Paths helper class:

```java
Path path1 = Paths.get("/home");
Path path2 = Paths.get(args[0]);
Path path3 = Paths.get(URI.create("file:///Users/user/file.java"));
```

Paths helper is shorthand for `FileSystems.getDefault().getPath(String);`

Notes (source [java nio File Paths helper class](https://docs.oracle.com/javase/7/docs/api/java/nio/file/Paths.html)):

- Confusingly, the Paths Helper Class has two static members `Path()`
- Convert a path string or sequence of strings to a Path object: `public static Path get(String first, String...)` :right-arrow: Best used with Path.resolve helper e.g. `Path dir=""; Path path=dir.resolve("file");`
- Convert a URI to a Path object: `public static Path get(URI uri)` :right-arrow: Iterates over installed providers to find one that handles the URI scheme.

Create a file and get a reference to it in either Unix or Windows:

```java
Path myFile = Paths.get(System.getProperty("user.home"), "logs", "logfile.txt");
```

Path syntax _can be bound to the underlying OS sematics_ but it might be better to use Environment Variables and Path instance methods to get info:

```java
Path path = Paths.get("/home/username/log-file.log");
path.toString(); // /home/username/log-file.log
path.getFileName(); // log-file
path.getName(0); // /home
path.getNameCount(); // count of elements in path: 3
path.subpath(0,2); // /home/username
path.getParent(); // /home/username
path.getRoot(); // The root path: /
path.normalize(); // removes redundant indicators like . and .. from the path
```

Key takeaway: `Path` class contains methods for manipulating a path.

#### Converting a Path

Three methods to do so:

```java
Path path1 = Paths.get("/home/users");
path.toAbsolutePath(path1); // /home/users
Path userInputPath = Paths.get(args[0]);
path.toAbsolutPath(userINputPath); // /root/pathOfExecutable/userInputPath
```

`toRealPath()`: Returns the _real_ path of an existing file:

- Resolves symlinks.
- Extends relative to fully qualified path.
- Removes redundant elements.

_Note_: Leverage _NoSuchFileException_ to catch errors related to Path and Paths operations.

Join Paths using `Paths.get("path_one").resolve("child_path")`.

Use Relativize method to return the path to a sibling path from a starting path:

```java
Path p1 = Paths.get("foo");
Path p2 = Paths.get("bar");
Path p1_to_p2 = p1.relativize(p2); // ../bar
Path p2_to_p1 = p2.relativize(p1); // ../joe
// use this to avoid typing stuff like Paths.get("../../grandParentPath/baz")
```

_Note_: Relative paths might be a problem for Relativize depending on the root path and the OS.

Compare Two Paths using equals:

```java
path.equals(otherPath); // returns boolean if path equals otherPath
path.startsWith(beginning); // returns boolean of Path root is equal to "beginning"
path.endsWith(ending); // returns boolean of Path last-child is equal to "ending"
```

Path implements:

- Iterable interface: Can be used with For and Advanced For loops.
- Comparable interface: Can be sorted.
- Equals method: Helper methods `compareTo()` and `isSameFile()` (two paths locate the same file) are exposed.

#### File Operations

`Files` class is a `java.nio.file` package entrypoint.

- Static Methods
- Read, Write, Manipulate files and directories
- Work with `Path` objects.

Terminology:

- Releasing System Resources: Many classes impelment or extend `java.io.Closeable` interface. This is used to limit memory leaks. Use-with-resources is a common way to do this. Another is to call an Object's `close()` method before leaving an execution scope.
- Exceptions: Use Try-Catch-Finally blocks or Try-with-resources to surround code that could throw Exceptions. For file operations, `IOException` is common. Use `.close()` method within a Finally block if the object is null.
- Varargs: Stands for Variable Number of Arguments. Example `Path Files.move(Path, Path, CopyOption...)` where `...` means pass-in a comma-separated list of values. `CopyOption[]` would mean to pass-in an array of type CopyOption instances.
- Atomic Operations: `move()` method is atomic meaning all-or-nothing operation. Success or failure, no in-between.
- Method Chaining: A method that returns an object can have a 'chained method' that can act on that returned object. Example `String value = Charset.defaultCharset().decode(buf).toString();`.
- Globs: A String-type that can be matched against other Strings (including Director and File names). Rules for Globs are below.
- Link Awareness: Method knows what to do with Symbolic Links, and allows adding flags to indicate what to do with a Symlink.

Key Takeaways on Files class methods:

- Move files.
- Copy files.
- Delete files.
- Retreive file attributes.
- Set file attributes.

##### Globs Rules

Glob syntax rules:

- An asterisk: Match any number of characters or none.
- Two asterisks: Asterisk that crosses directory boundaries (e.g. complete path matching).
- Question Mark: Match a single character only.
- Braces: Collection of subpatterns. `{temp*, tmp*}`.
- Brackets: Set of single characters, or a range when used with a dash `[abcdefg]` or `[0-9]`.
- Character: Match themselves (`* ? \` match themselves within brackets).
- Escape character: `\`. Use `\\` to match a single `\` character.

Note: Command-line escape characters might differ between systems.

Consider Globs to be like RegEx syntax that `java.nio.file` understands.

#### Checking a File or Directory

Verify existence!

- `exists(Path, LinkOption...)`
- `notExists(Path, LinkOption...)`

Three possible results:

- Verified to exist.
- Verified to NOT exist.
- Status is unknown e.g. access denied, etc.

File Accessibility:

- `isReadable(Path)`: Boolean
- `isWriteable(Path)`: Boolean
- `isExecutable(Path)`: Boolean

_Note_: TOCTTOU (Tock-too) errors can occur when testing for Read, Write, and Executability and then accessing the file. Read about how to avoid this situation.

Two Paths Can Locate The Same File!

- Symlinks
- `isSameFile(Path, Path)`: Boolean

#### Deleting Files Directories and Links

Files and Directories:

- File is actually removed from the file system.
- Directory will only be deleted if empty.

Symlinks:

- Only the Symlink is removed, not the target items.

Deletion Methods:

- `delete(Path)`: Succeeds or throws an Exception.
- `deleteIfExists(Path)`: Use when multiple threads could be deleting same path/item. Silently fails.

#### Copying Files and Directories

`copy(Path, Path, CopyOption...)`

- Fails if target file exists and `REPLACE_EXISTING` NOT specified.

CopyOption Enums/Varargs:

- REPLACE_EXISTING: Copies over existing target. Symlinks are copied (not the target). Throws `DirectoryNotEmptyException`.
- COPY_ATTRIBUTES: File attributes are OS-specific but 'last-modified-time' is universal and is automatically copied.
- NOFOLLOW_LINKS: Do NOT follow Symlinks. If specified path IS a Symlink, copy the Symlink itself but not the Symlink target.

Example:

```java
import static java.nio.file.StandardCopyOption.*;
Files.copy(source, target, REPLACE_EXISTING);
```

_Note_: `Files.walkFileTree()` method supports recursive copying.

#### Moving Files and Directories

`move(Path, Path, CopyOption...)`: Same failure mode as Copying.

CopyOption Enums/Varargs:

- REPLACE_EXISTING: Overwrite target path. Symlink target will get overwritten (but not its target).
- ATOMIC_MOVE: Perform move as an atomic 'all-or-nothing' operation. Throws if File System does not support Atomic operations.

Example:

```java
import static java.nio.file.StandardCopyOption.*;
Files.move(source, target, REPLACE_EXISTING);
```

#### Managing Metadata

Filesystem metadata is stored IN files and directories.

AKA File Attributes.

See [Oracle Java Docs File Attributes](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) for methods that act of Filesystem Metadata.

Metadata is collected into Views so that effectively similar information can be displayed, whether POSIX or DOS style Filesystem:

- `BasicFileAttributeView`
- `DosFileAttributeView`
- `PosixFileAttributeView`
- `FileOwnerAttributeView`
- `AclFileAttributeView`
- `UserDefinedFileAttributeView`

_Note_: Not all views are supported by all systems, and some file systems support views NOT supported in java.nio.file libraries.

FileAttributeView interfaces can be accessed via `getFileAttributeView(Path, Class<V>, LinkOption...)` but in most cases is not necessary.

Some FileAttributes can be programmatically set. See [Oracle Java Docs File Attributes](https://docs.oracle.com/javase/tutorial/essential/io/fileAttr.html) for methods and usage.

#### Reading, Writing, Creating, and Opening Files

Utility Methods for simpler, common cases:

- readAllBytes: Read-in a small file in a single pass.
- readAllLines
- Write methods such as `Files.write(file, buf)`

Iteration over a stream or lines of text and interop with java.io package (which includes Buffered Streaming capability):

- newBufferedReader
- newBufferedWriter
- newInputStream
- newOutputStream

More complex, less common methods:

- ByteChannels
- SeekableByteChannels
- ByteBuffers
- newByteChannel

Locking and memory-mapped IO required:

- FileChannel

OpenOptions Parameter:

- Many methods utilize this.
- API will state what default is if not supplied to the method.
- Many Enums supported (see list on [Oracle Docs File](https://docs.oracle.com/javase/tutorial/essential/io/file.html)).

#### Methods for Unbuffered Streams and Interop with java.io APIs

Reading File with Stream IO:

- `newInputStream(Path, OpenOption...)`: Returns unbuffered input stream for oreading bytes from a file. Wrap an instance of `InputStream` with a `BufferedReader` instance.

Creating, Writing File with Stream IO:

- `newOutputStream(Path, OpenOption...)`: Returns an unbuffered output stream. Utilize OpenOption Enums to flag specific behavior e.g. `CREATE, APPEND`, etc.

#### Methods for Channels and ByteBuffers

Two methods for reading and writing channel IO:

- `newByteChannel(Path, OpenOption...)`
- `newByteChannel(Path, Set<? extends OpenOption>, FileAttribute<?>...)`

These return an instance of a `SeekableByteChannel` that can be cast to a `FileChannel` which can allow mapping file contents to memory for faster access.

Key Takeaway: _To seek to a specific location in a file and read it_, use `Files.newByteChannel` and its returned instance of `SeekableByteChannel` to read/write from/to any position within a file.

See [Oracle Docs File](https://docs.oracle.com/javase/tutorial/essential/io/file.html) for more (there is a lot).

#### Methods for Creating Regular and Temporary Files

`createFile` is an atomic operation method.

There example code of how to create a file with default attributes using createFile().

For temporary files, use:

- `createTempFile(Path, String, String, FileAttribute<?>)`: Specify a temporary file location.
- `createTempFile(String, String, FileAttribute<?>)`: Use File-system Default temp location.

See [Oracle Docs File](https://docs.oracle.com/javase/tutorial/essential/io/file.html) for an example.

### Random Access Files

Non-sequential access to file contents.

1. Open
2. Seek to location
3. Read from (or write to) the file

SeekableByteChannel interface provides a Channel I-O.

SeekableByteChannel API Methods:

- `position`: Returns current position.
- `position(log)`: Sets current position.
- `read(ByteBuffer)`: Reads bytes into buffer.
- `write(ByteBuffer)`: Writes bytes from buffer.
- `truncate(long)`: Truncates a file (or entity) connected to the channel.

`Path.newByteChannel` methods return an instance of SeekableByteChannel.

SeekableByteChannel can be cast to `FileChannel` providing advanced features: Mapping a region to memory, locking a region of a file, and reading/writing bytes from an absolute position.

There is a [code snippet](https://docs.oracle.com/javase/tutorial/essential/io/rafs.html) that demonstrates the use of `ByteBuffer`, `FileChannel`, `position`, `rewind`, `nread`, and `write`.

#### Creating and Reading Directories

`FileSystem` Class contains a variety of methods for obtaining information about the file system.

List Directories:

- `FileSystem.getRootDirectories()`: Implements Iterable interface.
- Chain `getDefault().getRootDirectories()` for directories in Root.

Create a Directory:

- `Files.createDirectory(Path, FileAttribute<?>)`: Without FileAttribute, a default set of attirbuites will be applied.
- Attributes are listed like `"rwxr-x---"` e.g. `Set<PosixFilePermissions> perms = PosixFilePermissions.fromString("rwxr-x---");`
- Directory creation is NOT atomic and can fail with partial work completed.

Create a Temporary Directory:

- `createTempDirectory(Path, String, FileAttribute<?>...)`: Allows code to specify a location for the temp directory.
- `createTempDirectory(String, FileAttribute<?>...)`: Creates a new directory in the default temporary-file directory.

Listing Directory Contents:

- `newDirectoryStream(Path)`: Implements DirectoryStream interface, which implements Iterable.
- Example: `DirectoryStream<Path> stream = Files.newDirectoryStream(dir))...`

Be sure to use Try-with-resources because the returned DirectoryStream _is a Stream_.

Everything including files, links, subdirectories, and hidden files will all be returned unless Globbing is used:

`DirectoryStream<Path> stream = Files.newDirectoryStream(dir, "*.{java,class,jar}"))` etc.

#### Writing Directory Filters

Use `DirectoryStream.Filter<T>` interface, method `accept()`:

Create Filter partial example: `DirecotryStream.Filter<Path> filter = newDirectoryStream.Filter<Path>() { public boolean accept(Path file) throws IOException { ... }}`

Invoke custom Filter partial example: `try (DirectoryStream<Path> stream = Files.newDirectoryStream(dir, filter)) { ... }`

See Oracle's Java Documentation on [Writing Your Own Directory Filter](https://docs.oracle.com/javase/tutorial/essential/io/dirs.html) for the full example.

#### Symbolic and Other Links

`java.nio.file` package supports links and behavior can be configured when a Symlink is discovered.

Notes about Hard Links:

- Opposite of Symlinks or 'soft' links.
- Target of the link must absolutely exist.
- Not allowed on directories.
- Not allowed to cross partitions or volumes.
- Are more similar to a regular file in looks and behavior.
- Carry same metadata (identical) as the target.
- Path methods work with them seamlessly.

Create a Symbolic Link:

- `createSymbolicLink(Path, Path, FileAttribute<?>)`: Path1 = newLink; Path2 = target.
- FileAttributes vararg works as with other java.nio.file package objects.

Create a Hard Link:

- `createLink(Path, Path)`
- Throws NoSuchFileException if Path2 does not point to an actual file.

Detecting a Symlink:

- `isSymbolicLink(Path)`

Finding Link Target:

- `readSymbolicLink(Path)`
- Throws NotLinkException if Path is not a Symlink.

Key Takeaway: Detect Symlinks by using `java.nio.file` package `File` instanace `.isSymbolicLink(Path)` for a boolean result.

#### Walking The File Tree

FileVisitor Interface:

- Implement `FileVisitor` to detmine behavior through traversal process.

FileVisitor Traversal Behavior Methods:

- `preVisitDirecotry`: Invoked before directory entries are visited.
- `postVisitDirectory`: Invoked after all entries in directory are visited. Exceptions are passed to this method.
- `visitFile`: Invoked _on the file being visited_ and returns BasicFileAttributes to the method. FileAttributes package can be used to read specific attributes.
- `visitFileFailed`: Invoked when the file cannot be accessed and an Exception is passed to the method for handling (throw it, log it, etc).

Review [FileVisitor Interface](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) documentation on Oracle JavaSE Docs for examples and more info.

Initiating a Traversal with these Methods and options enum:

- `walkFileTree(Path, FileVisitor)`: Path is starting point, FileVisitor is your FileVisitor instance.
- `walkFileTree(Path, Set<FileVisitOption>, int, FileVisitor)`: Enables specifying limit on number of levels to visit via `FileVisitOptions` enums.
- `FOLLOW_LINKS`: A FileVisitOptions enum that enables following Symlinks.

FileVisitor Considerations:

- Traversal is Depth-First.
- Child directories are not in a name-based sort order.
- Files and Directories could be changed by other applications or services while FileVisitor is traversing.
- In recursive file copy, attribute copying is a _2nd step_ in the process. Requires using `preVisitDirectory`, `visitFiles`, and `postVisitDirectory`
- Using `visitFile` to perform a file search does not find Directories. To get direcotories, perform a comparison in either `preVisitDirectory` or `postVisitDirectory` methods.
- Avoid following Symlinks when _deleting_ files (could produce unsavory results).
- `walkFileTree` does _not follow_ Symlinks.
- `visitFile` method is invoked for _files_. If configured to follow Symlinks, recursive/loop discoveries will be reported in `visitFileFailed` method with `FileSystemLoopException`

Controlling the Flow of FileVisitor:

FileVisitor methods return a `FileVisitResult` value where you control the flow of the traversal:

- CONTINUE: Direcotry is 'visited' if CONTINUE is returend by `preVisitDirectory` method.
- TERMINATE: When returned the traversal stops immediately.
- SKIP _SUBTREE: Specified directory (and sub-directories) are \_skipped_ when `preVisitDirectory` method returns this value.
- SKIP_SIBLINGS: When returned by `preVisitDirectory` method, `postVisitDirectory` method is not invoked and neither the specified directory nor its siblings will be visited.

Check out [Controlling the Flow Code Snippets and Examples at page bottom](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) at Oracle JavaSE Docs.

#### Finding Files

Use pattern matching to help, i.e. `*` for any, `?` for single placeholder, etc.

File System implementations in `java.nio.file` provides a `PathMatcher` functionality.

PathMatcher accepts Glob or Regular Expressions as the the params to `.getPathMatcher()`.

Steps to use:

1. Create a PathMatcher instance.
2. Match files against it.

```java
PathMatcher matcher = FileSystems.getDefault().getPathMatcher("glob:*.{java, class});`
Path filename = ...;
if (matcher.matches(filename)) {
  System.out.println(filename);
}
```

Example java taken directly from the Finding Files section of _[javase tutorials on essential io]_

Recursive pattern matching is used to find a file _somewhere_ within a file system.

- Search by parts of a filename.
- Search by file extension.

Use `Find` with a glob pattern to search the file system for a file.

The Find class:

- Is a Console App (has a Main() entry point that instantiates the internal Finder class).
- Extends `SimpleFileVisitor<Path>`
- Leverages `PathMatcher` as a field and the input args are used to set up the `pattern` for pattern matching.
- Is instantiated using a String pattern, which initializes a PathMatcher with a glob pattern from the CTOR param.
- Adds `@Overrides` that define `preVisitDirectory()`, `visitFileFialed()`, and `visitFile()` (all FileVisitor traversal behavior methods).
- Calls `walkFileTree()` (Find is a simple FileVisitor polymorphism).
- Returns the field `count` for the number of matching files found while walking the file tree.

#### Watch a Directory for Changes

Utilize functionality called 'file change notification'.

- Detect operations on a relevant directory in the file system.

Detection through file system changes is inefficient, so `java.nio.file` has an API for that:

- Enables registering directory/ies with a Watch service.
- Enables settings they _type of operation_ to watch for e.g. ENTRY_CREATE, ENTRY_DELETE, and/or ENTRY_MODIFY.
- Process is 'called back' by the API when an event is detected.

There is also an OVERFLOW event, but registration is not required in order to receive it (probably an unchecked exception escape hatch).

Oracle recommends caution when deciding to implement their 'Watch Service API' referenced in the documentation:

- Not for indexing a file system.
- Most (but not all) file systems support change notification, and the Watch Service API takes advantage when it exists.
- Without file-system-based notification, the Watch Service will _poll the file system_ to detect the events.

#### Determining MIME Types

Use `probeContentType(Path)` to get a file's MIME Type:

```java
try {
  String type = Files.probeContentType(filename);
  if(type==null) {
    System.err.format("%s has an unknown filetype.%n", filename);
  } else if (!type.equals("text/plain")) {
    System.err.format("%s is not a plain text file.%n", filename);
    continue;
  }
  catch (IOException ioex) {
    System.err.println(ioex);
  }
}
```

Return is either String or null (if cannot be determined).

Content Type is generally managed by the platform's type detector, so presumptive content-types like: Extension `.class` is a Java file, might not be correct.

Take a look at [FileTypeDetector](https://docs.oracle.com/javase/8/docs/api/java/nio/file/spi/FileTypeDetector.html) in the Oracle Java Docs. Note that it still 'guesses'.

#### Default File System

Use `FileSystems.getDefault()` method and chain it with `FileSystem` type methods. Example:

```java
PathMatcher matcher = FileSystems.getDefault().getPathMatcher("glob:*.*");
```

#### Path String Separator

Path separators are not always the same:

- Windows: `\`
- POSIX: `/`
- Others: (could be different still)

Retreive the path separator character using:

- `String separator = File.separator;` or
- `String separator = FileSystems.getDefault().getSeparator();`

#### File System Stores

Files and Directories are actually stored within a File System's _Stores_.

`File Store` represents the underlying storage device:

- Windows: Volumes with alpha-labels e.g. 'C'
- UNIX: A mounted File Store.

List all file stores the system has:

```java
for (FileStore store: FileSystems.getDefault().getFileStores()) {
  ...
}
```

Get a specific File Store:

```java
Path file = ...;
FileStore store = Files.getFileStore(file);
```

#### Legacy File IO Code

Prior to Java SE 7:

- `java.io.File` was used.
- Inconsistent Exception throwing.
- Inconsistent rename handling.
- No SymLink support.
- Lack of MetaData support.
- Inefficient algorithms and classes, especially for large-scale calls.
- Unreliable circular-link detection.

##### Migrating to NIO

`java.io.File.toPath()` converts File instance to `java.nio.file.Path` instance: `Path input = file.toPath();`

There is a large matrix of functionality that relates `java.io.File` functionality to `java.nio.file` Functionality, along with links to tutorials on usage at [Oracles Java Docs on File IO](https://docs.oracle.com/javase/tutorial/essential/io/legacy.html).

### Oracle Tutorial Q and A

What Class and method would you use to read a few pieces of data that are at known positions near the end of a large file?

> Use `Files.newByteChannel` to get instance of `SeekableByteChannel` which allows reading from/writing to any position in a file.

When invoking `format`, what is the best way to indicate a new line?

> Use `%n`which is platform independant.

How would you determine the MIME type of a file?

> Two options: Use `Files.probeContentTypes(Path: file_name)` (which uses the file systems underlying file type detector). Note: Oracle suggested an optional `FileTypeDetector` code file to try.

What method(s) would you use to determine whether a file is s symbolic link?

> Use `Files.isSymbolicLink(Path: file_name)` method.

Note:

- Use `Paths` class method `.toRealPath(Path: symlink_name)` to get the actual path to a Symlinked file.

## Notes from Baeldung Readings

### Creating Streams

- Use `Stream.empty()` to create a new Stream and test whether it is empty before tryingn to use it.
- Create as a collection e.g. `Collection<Integer> numbersStream = Arrays.asList(1, 2, 3); Stream<Integer> streamOfNumbers = numbersStream.stream();`
- Create a Array stream `Stream<Integer> streamOfArray = Stream.of(1, 2, 3);`
- Stream Of Array can be initialized with an existing Array or a combination of new elements _and_ an existing Array.
- Use `Stream.builder()` with a type hint and a size (otherwise is 'infinite'): `Stream<Integer> generatedStream = Stream.Generate(()->1).limit(5);`
- Another infinite Stream: `Stream<Integer> iterStream = Stream.iterate(1, num-> num * 2).limit(4);` :arrow_right: `1, 2, 4, 8`
- Stream of Primitives (Java 8): int, long, and double. Implements `IntStream`, `LongStream`, and `DoubleStream`.
- Stream of String: Leverage `chars()` method, which produces Integer representations of characters (example below).
- File Stream: Using `lines()` method, `Java.NIO.Files` class supports streaming file data (example below).

Examples:

```java
// Stream of String (of Integer representation of Characters)
IntStream streamOfChars = "word".chars();
// use RegEx
Stream<String> streamOfString = Pattern.compile(", ").splitAsStream("X", "Y", "Z");
```

```java
// Stream of File (of Strings)
Path path = Paths.get('C:\\example.txt');
Stream<String> streamOfStrings = Files.lines(path);
Stream<String> streamWithCharset = Files.lines(path, Charset.forName('UTF-8'));
```

_[Java 8 Streams at [Baeldung.com](https://www.baeldung.com/java-8-streams)]_

### Referencing Streams

- Only _intermediate_ operations are allowed on an instantiated Stream.
- "Terminal" operations render the Stream inaccessible: `stream.findAny()` is an example of a method that will work but an IllegateStateException will be thrown (a RuntimeException). This is tricky because it `will not be caught at design or compile time`.
- Proper way is to encapsulate the Stream using a Collection like `List<T>` and the `collect(Collectors.toList())` nested methods.

```java
List<String> elements = Stream.of("X", "Y", "Z")
  .filter(element -> element
  .contains("Y"))
  .collect(Collectors.toList());
Optional<String> anyElement = elements.stream().findAny();
Option<String> firstElement = elements.stream().findFirst();
```

### Stream Pipelines

Sequence of operations for using Streams:

1. Source: Where the data will be streamed from, e.g. an Array.
2. Intermediate Operations: Return a new, modified Stream. Can be chained. `skip()`, `map()`, and others.
3. Terminal Operation: Only one is allowed per Stream. Returns a result of operations done on the Stream.

```java
List<String> list = Arrays.asList("alpha", "bravo", "charlie");
long size = list.stream().skip(1).map(item -> item.substring(0, 3)).sorted().count()
```

TODO:

- [ ] Look up actual definitions of Source, Intermediate Operation, and Terminal Operation and record information here.

### Lazy Invokation

- Intermediate operations are lazy - only execute _if needed by Terminal Operation_.
- Terminal operations (such as `map()`) force the Intermediate operation(s) to execute and produce results.
- Method calls that are not required for by the Terminal operation _are never called_.

### Order of Execution

- Chaining operations in correct order will produce correct result.
- Intermediate operations that reduce the size of the Stream should be placed before operations that apply to each element.
- Place `skip()`, `filter()`, and `distinct()` at the top of the Stream pipeline.

### Stream Reduction

- There are many Terminal operations including: `count()`, `max()`, `min()`, and `sum()`.
- Reduction mechanisms like these can be customized using `reduce()` and `collect()`.

#### Reduce Method

Variations:

- Identity: Initial value or default value if Stream is empty.
- Accumulator: Logic that aggregates elements, returning a new value at each reducer iteration. A poor performer in some circumstances.
- Combiner: Aggregates Accumulator results. Useful for parallel operations from other threads.

```java
OptionalInt reduced = IntStream.range(1, 4).reduce((a, b) -> a + b);
// 1+2, 3+3 returns 6
```

```java
int reducedTwoparams = intStream.range(1, 4).reduce(10, (a, b) -> a + b);
// 10 + 1 + 2, 13 + 3 returns 16
```

```java
int reducedParams = Stream.of(1, 2, 3)
  .reduce(10, (a, b) -> a + b, (a, b) -> {
    log.info("combiner was called");
    return a + b;
  });
  // combiner will not be called in non-parallel reducers
  // however result is still 16
```

```java
int reducedParallel = Arrays.asList(1, 2, 3)
  .parallelStream()
  .reduce(10, (a, b) -> a + b, (a, b) -> {
    log.info("combiner was called");
    return a + b;
  });
// combiner called twice and result is 36
// each combiner processing happens in parallel
// 10 + 1 and 10 + 2 and 10 + 3
// so when accumulated is 11, 12, and 13
// and when combined is 11 + 12 + 13 result 36
```

_[Java 8 Streams at [Baeldung.com](https://www.baeldung.com/java-8-streams)]_

#### The Collect Method

- Is a Terminal operation.
- Accepts argument of type Collector.
- Collector specified reduction mechanism.
- Many types of Collectors already exist.

Steps:

1. Start with a `List<T>` and init as `Arrays.asList(new {type(value)}, new {type(vlaue)})` to init or add elements of 'type' into a List.
2. Convert to a Collection, List, or Set using `.stream().map(MyType::getName).collect(Collectors.toList());`.
3. Operate on the Collection using `.collect(Collectors.command(args))`.

Tools:

- Reduce to String using `.stream().map(MyType::getName).collect(Collectors.joining(", ", "[", "]"));` (args: delimiter, prefix, suffix).
- Find average value of elements: `.stream().collect(Collectors.averagingInt(MyType::getValue));` (getValue is getter method on MyType).
- Sum all elements: `.stream().collect(Collectors.summingInt(MyType::getValue));` (getValue is getter on MyType).
- Summarizing statistic: `.stream().collect(Collectors.summarizingInt(MyType::getValue));`. Follow with `toString()` for output.
- Grouping elements per specific function: `.stream().collect(Collectors.groupingBy(MyType::getValue));`
- Grouping by predicate: `.stream().collect(Collectors.partitioningBy(item -> item.getValue > minValue));`
- Additional Transformation: `.stream().collect(Collectors.collectingAndThen(Collectors.toSet(), Collection::unmodifiableSet));` which will convert Stream to Set, then Set to immutable Set.

Custom Collectors can be created using `of()` method of type `Collector`:

```java
Collector<MyType , ?, LinkedList<MyType>> toLinkedList = Collector.of(LinkedList::new, LinkedList::add, (first, second) -> {
  first.addAll(second);
  return first;
});
LinkedList<MyType> linkedListOfMythings = listOfMyThings.stream().collect(toLinkedList);
// Collector instance gets reduced to the LinkedList, first element?
```

#### Parallel Streams

Java 8 makes things simpler with:

- ExecutorService
- ForkJoin

Create parallel Streams when source is a Collection or an Array type, using `parallelStream()` method:

```java
Stream<MyType> streamOfCollection = myTypes.parallelStream();
boolean isParallel = streamOfCollection.isParallel();
boolean bigInstance = streamOfCollection
  .map(myTypeItem -> myTypeItem.getValue() * someValue)
  .anyMatch(thisValue -> thisValue > 200);
```

Create parallel Streams using `parallel()` when source is _not_ a Collection or an Array type:

```java
IntStream intStreamParallel = IntStream.range(1, 100).parallel();
boolean isParallel = intStreamParallel.isParallel();
```

Notes:

- ForkJoin is used automatically and does not need to be written.
- Common thread pool is used so custom assigning threads is not possible (unless using custom set of parallel collectors).
- Avoid blocking operations!
- Tasks that take similar amount of execution time should be used for best results.

Convert Parallel Mode Stream back to sequential mode using `sequential()`:

```java
IntStream intStreamSequential = intStreamParallel.sequential();
boolean isParallel = intStreamSequential.isParallel();
```

_[Java 8 Streams at [Baeldung.com](https://www.baeldung.com/java-8-streams)]_

#### Memory Leaks

Always apply `close()` to terminal operations to avoid memory leaks.

Unconsumed Streams will create memory leaks.

## Stream FindAny and FindFirst

See [Baeldung Streams FindAny and FindFirst](https://www.baeldung.com/java-stream-findfirst-vs-findany)

### Stream FindAny

Find any element within a Stream.

- Order is ignored.
- Returns an `Optional` instance which is empty if the Stream is empty.
- Can be parallelized.
- Not guaranteed to return the 1st element that matches.
- Parallelized operations may return results that are indeterminate. Use `anyOf(is(a), is(b), ...)` to allow for empty returns mixed with truthy returns.

### Stream FindFirst

Find the first element in a Stream.

- Does not have a defined 'encounter order'.
- Relies on the source Stream and Intermediate Operations to determine encounter order.
- Return type is `Optional` which is empty if the Stream is empty.
- Can be parallelized.
- Behavior when parallelized _does not change_ from synchronous.

## Streams Functional Interfaces in Java 8

See [Baeldung Java8 Streams Functional Interfaces](https://www.baeldung.com/java-8-functional-interfaces)

[Baeldung Lambda Expressions and Functional Interfaces Tips and Best Practices](https://www.baeldung.com/java-8-lambda-expressions-tips).

### Lambda Expressions

- aka 'Lambdas'
- New in Java 8.
- An anonymous function.
- Can be passed to a method as an argument.
- Can be returned by a method as a functional object.
- Useful to represent primitive functions or data types, without all the formalities of creating a concrete class.

### Functional Interfaces

- Requires `@` annotation.
- Any Interface with a Single Abstract Method (SAM) is a Functional Interface.
- Implementation can be treated as if it were a Lambda Expression.

_Note_: Default Methods do not count as Abstract.

### Functions

Simple description: Interface with single method takes single value and returns single value `public interface Function<T, R> { ... }`.

Example of Standard Library Function Type: `Map.computeIfAbsent()`

- Returns value from a Map by Key only if present, otherwise returns calculated value.
- Represented in the java code, below:

```java
myHashMap.computeIfAbsent(string, (item) -> item.length);
// looks for key String and if not found inserts String into map with value item.length
```

Converting to a functional interface:

```java
myHashMap.computeIfAbsent(string, String::length);
// the pair of colons means think of this as a lambda function
```

Function Interface has default `compose()` method.

- Combines several functions into one.
- Executes functions sequentially.

How to:

1. Define a Function that uses Functional Interface `::`.
2. Define a Function that is a lambda that uses the addition operator to concatenate quoted strings and primitives that have default `toString()` method.
3. Define a Function that is the result of calling Function2 with the compose function, passing in Function1: `Function2.compose(Function1)`.

Very abstract. Here's _[The example from Baeldung.com]_ with comments added by me:

```java
// function uses Functional Interface and stores an Integer, returns a String
Function<Integer, String> intToString = Object::toString;
// function uses lambda and stores String input, returns a String output
Function<String, String> quote = s -> "'" + s + "'";
// function calls intToString, passing in quote and executes its built-in compose() method
Function<Integer, String> quoteIntToString = quote.compose(intToString);
// use assertion to verify output is as expected
assertEquals("'5'", quoteIntToString.apply(5));
```

### Primitive Function Specializations

Primitives cannot be generic type arguments.

Function Interface has ability to use `double`, `int`, `long`, and combinations thereof.

- IntFunction, LongFunction, DoubleFunction: Arguments are int, long, or double. Return type is parameterized.
- ToIntFunction, ToLongFunction, ToDoubleFunction: Return type specific. Arguments are parameterized.
- DoubleToIntFunction, DoubleToLongFunction (etc): Both argument and return type are as defined by their names. Available for all combinations of transformation.

Returning another Primitive Type from a Primitive Function can be achieved using a Functional Interface decorator/attribute, and implementing a custom function.

Example from _[Baeldung.com]_ with my comments added:

```java
@FunctionalInterface
public interface ShortToByteFunction {
  // a single method in the functional interface takes a single value and returns a single value
  byte applyAsByte(short s);
}

// allow passing in a Lambda Expression using ShortToByteFunction interface
public byte[] transformArray(short[] array, ShortToByteFunction function) {
  byte[] transformedArray = new byte[array.length];
  // step through each element in input array and apply the custom function interface method
  for (int i = 0; i < array.length; i++) {
    transformedArray[i] = function.applyAsByte(array[i]);
  }
  return transformedArray;
}
```

```java
// transform an array of shorts to an array of bytes multiplied by 2
short[] array = {(short) 1, (short) 2, (short) 3};
byte[] transformedArray = transformedArray(array, s -> (byte) (s * 2));
byte[] expectedArray = {(byte) 2, (byte) 4, (byte) 6};
assertArrayEquals(expectedArray, transformedArray);
```

This is an excellent example of why an Interface is important in object oriented programming. If any function was passed in but did not have the `.applyAsByte(short s)` method, the code would not compile.

### Two-Arity Function Specializations

[Two-Arity Function Specializations at Baeldung.com](https://www.baeldung.com/java-8-functional-interfaces#Specializations)

Define lambdas with 2 input args using library functions with "Bi" in the name.

- BiFunction: Generics used for input and output.
- ToDoubleBiFunction: Allows use of Primitives.
- ToIntBiFunction: Primitives allowed.
- ToLongBiFunction: Primitives allowed.

When using a Map function (or Map-like for e.g. `HashMap.ReplaceAll()`), a Two-Arity function can allow processing 2 values and returning a single result that the `ReplaceAll()` function proceses to elements in the HashMap.

### Suppliers

A Function Specialization that takes zero arguments.

Commonly used for lazy-generation or values.

Returns a Supplier type that can then be treated as a Stream object, and the 'state' values are treated as _final_.

Available Suppliers:

- BooleanSupplier
- DoubleSupplier
- LongSupplier
- IntSupplier

### Consumers

A 'void' type Function that accepts Generic Inputs.

Useful for generating _side effects_ e.g. Console output.

Built-in Consumer functions:

- DoubleConsumer
- IntConsumer
- LongConsumer
- BiConsumer types: Accepts two arguments.

### Predicates

Function that accepts one (Generic Type) value, and returns a Boolean.

Using a lambda like `.filter(n -> f(x))` within chained Stream functions provides a predicate (true/false) result that following chained functions that would operate when the predicate returns `true`.

Variations that accept primitive arguments:

- IntPredicate
- DoublePredicate
- LongPredicate

### Operators

Functions that receive and return the same value type.

Unary Operators `++` and `--` are examples.

- Prefixing a variable with a unary operator causes the function to execute 1st, returning the result of the operation.
- Postfixing a variable with a unary operator causes the function to return the input value 1st, then execute the operation.

From [W3Schools](https://www.w3schools.in/java/operators/unary), with comments added by me:

```java
public class unaryop {
 public static void main(String[] args) {
  int r = 6;
  // prints 6, stores 7 into variable r
  System.out.println("r=: " + r++);

  // print 7
  System.out.println("r=: " + r);

  int x = 6;
  // prints 6, stores 5 into variable x
  System.out.println("x=: " + x--);

  // prints 5
  System.out.println("x=: " + x);

  int y = 6;
  // stores 7 into variable y then prints 7
  System.out.println("y=: " + ++y);

  int p = 6;
  // stores 5 into variable p then prints 5
  System.out.println("p=: " + --p);
 }
}
```

### Legacy Functional Interfaces

Generally speaking:

- Develop Lambdas following FunctionInterface as a guide to defining input, output, processing, and applying the correct Lambda to a functional interface.
- Within 'Concurrency APIs' are Interfaces 'Runnable' and 'Callable' interfaces.
- In Java8 these interfaces are decorated with `@FunctionalInterface` annotation.

## Key Takeaways

- Streams can be instantiated and have references to them using intermediate operations.
- A terminal operation will render a Stream inaccessible and should be the _last_ operation in a chain on a Stream.
- Streams cannot be re-used. Run-Time Exception `IllegalStateOperation` will result when accessing a Stream that has already had a terminal operation run against it.
- Streams are for _applying a finite sequence of operations to a source of elements_.
- Streams are _not_ for storing data.
- Operate on Stream elements using `functional style` operations.

Operate on a Collection, not the Stream itself:

```java
List<String> elements = Stream
  .of("X", "Y", "Z")
  .filter(element -> element.contains("Y"))
  .collect(Collectors.toList());
Optional<String> anyElement = elements.stream().findAny();
Optional<String> firstElement = elements.stream().findFirst();
```

## Resources

[Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/essential/io/index.html).

Baeldung [Java Streams Links and Information](https://www.baeldung.com/java-streams).

Baeldung [Java IO Tutorials](https://www.baeldung.com/java-io) (mostly about file system manipulation).

Baeldung [GitHub Repo of Lambda and FunctionInterface examples](https://github.com/eugenp/tutorials/tree/master/core-java-modules/core-java-lambdas)

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
