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

### File IO with NIO.2

Oracle Java Docs refers to JDK 8 release and java.nio.file package and its sub-packages in this sub-section.

The documentation reviews Paths, both relative and absolute, and Symbolic Links.

Unix-based Paths are not comparable to Windows-based Paths due to their native naming convention. However, both can be handled and processed by Java.

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

See [Oracle Docs File](https://docs.oracle.com/javase/tutorial/essential/io/file.html) for more (there is a lot).

#### Methods for Creating Regular and Temporary Files

`createFile` is an atomic operation method.

There example code of how to create a file with default attributes using createFile().

For temporary files, use:

- `createTempFile(Path, String, String, FileAttribute<?>)`: Specify a temporary file location.
- `createTempFile(String, String, FileAttribute<?>)`: Use File-system Default temp location.

See [Oracle Docs File](https://docs.oracle.com/javase/tutorial/essential/io/file.html) for an example.

### Randome Access Files

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

- `createLin(Path, Path)`
- Throws NoSuchFileException if Path2 does not point to an actual file.

Detecting a Symlink:

- `isSymbolicLink(Path)`

Finding Link Target:

- `readSymbolicLink(Path)`
- Throws NotLinkException if Path is not a Symlink.

#### Walking The File Tree

FileVisitor Interface:

- Implement `FileVisitor` to detmine behavior through traversal process.

FileVisitor Traversal Behavior Methods:

- `preVisitDirecotry`: Invoked before directory entries are visited.
- `postVisitDirectory`: Invoked after all entries in directory are visited. Exceptions are passed to this method.
- `visitFile`: Invoked _on the file being visited_ and returns BasicFileAttributes to the method. FileAttributes package can be used to read specific attributes.
- `visitFileFailed`: Invoked when the file cannot be accessed and an Exception is passed to the method for handling (throw it, log it, etc).

Review [FileVisitor Interface](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) documentation on Oracle JavaSE Docs for examples and more info.

Initiating a Traversal:

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

Check out [Controling the Flow Code Snippets and Examples at page bottom](https://docs.oracle.com/javase/tutorial/essential/io/walk.html) at Oracle JavaSE Docs.

## Resources

[Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/essential/io/index.html).

Baeldung [Java Streams Links and Information](https://www.baeldung.com/java-streams).

Baeldung [Java IO Tutorials](https://www.baeldung.com/java-io) (mostly about file system manipulation).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).
