# DotNET Task Parallel Library Notes

Notes taken while reviewing MSFT Learn documentation of Task Parallel Library (TPL).

## Overview

The Task parallel Library and PLINQ Execution Engine enable developing scalable code without having to work directly with threads or the thread pool.

TPL: Task Parallel Library. Provides parallel versions of `for` and `forEach` constructs, and the `Task` class.

PLINQ: Parallel LINQ. Parallel implemntation of 'LINQ to Objects' with performances enhancements.

Data Structures for Parallel Programming: Provides thread-safe collections, lightweight synchronization types, and types for Lazy initialization.

Parallel Diagnostic Tools: Enables visualization into parallel tasks in Visual Studio and the Concurrency Visualizer.

Data Parallelism: Same operations performed concurrently on elements of a source collection/array.

Interlocked: A `System.Threading` library, providing atomic operations for variables shared by multiple threads [Interlocked Class](https://learn.microsoft.com/en-us/dotnet/api/system.threading.interlocked?view=net-8.0).

Local State: A `Func<TResult>` variable that exists just before a Parallel operation, until just after execution, for capturing thread-local state e.g. an accumulating value resulting from the iterations.

Loop Logic: A delegate or lambda expressing e.g. `Func<int, ParallelLoopState, long, long>` that will be provided to each occurrence of the loop, and defines the conditions of the loop such as `counter`, last index, a thread local variable, and a return type. The last param is passed to `localFinally` (type: `Action<TLocal>`) delegate after last iteration completes.

Thread Local: TBD.

Partition Local: Similar to Thread Local but multiple partitions can run within a single Thread.

## TPL - Task Parallel Library

Public Types and APIs in `System.Threading` and `System.Threading.Tasks` namespaces.

Help developers simplify adding parallelism and concurrency to applications.

TPL:

- Dynamically scales concurrency.
- Enables use of all processors, efficiently.
- Handles partitioning work via ThreadPool threads.
- Supports Cancellation, statement mangaement, and other low-level details.
- Helps developers create high performing code without getting their hands too dirty.

## TPL - For and ForEach

Data from the source is partitioned so the iteration processes can happen concurrently.

Task Scheduler manages concurrency and system resources based on workload, and can redistribute work among multiple threads/processors.

```c#
// the collection is partitioned and the delegate
// passed in to individual threads for processing
Parallel.ForEach(collection, (arg) => { ... });
Parallel.For(int, (arg) => { ... });

// non-generic option:
Parallel.ForEach(nonGenericCollection.Cast<object>(),
  currentElement => {
    // process currentElement
  });
```

A custom Partitioner or Scheduler can be implemented and supplied to the TPL methods.

When accumulating a result from these looping structures, write `Interlocked` methods like `Add(ref total, obj subtotal)` to ensure thread-safe, atomic accumulator operations.

### For and ForEach Cancellation

Cancellation is supported using Cancellation Tokens.

Supply `CancellationToken` to the method in `ParallelOptions` parameter and enclose the call within a `try-catch` block.

Catching an `OperationCanceledException` allows implementation of cleanup code and any notifications before returning from the parallel operation.

_Note_: If some other Exception is thrown before `Cancel()` is called, an `AggregateException` will be thrown from the loop, encompassing any pre-cancelation Exception and the `OperationCanceledException` as instances in an inner exception collection.

### For and ForEach Exceptions

There is no special Exception handling within these methods in the TPL.

- Exceptions can 'cascade' between thread completions and should all be caught (chances are the 1st Exception causes many other Threads to throw as well).
- Use `ConcurrentQueue<Exception>` to capture Exceptions thrown by individual threads.
- Use `try-catch` and within the catch block: `catch (Exception ex) { exceptions.Enqueue(ex); }`.
- At the end of the method encapsulating the TPL loop, check for exceptions in the ConcurrentQueue and if there are any, throw them as `new AggregateException(exceptions);`.

## TPL - Create And Run Tasks Implicitly

Use `Parallel.Invoke`:

- Conveniently run any number of arbitrary code, concurrently.
- Pass-in `Action` delegates to launch the work to be executed concurrently.
- Delegate can be a lambda and can call some other method, rather than contain the code directly.

```c#
Parallel.Invoke(() => GetTheseThings(), () => SetThoseThings());
```

### TPL - Create and Run Tasks Explicitly

- Can provides more control by leveraging the TAP library.
- Work is represented by `Task` or `Task<TResult>` classes.
- Encapsulate the work in a lambda expression and the Task will execute.
- `Task.Run()` is preferred way to create and launch a Task in one line.
- `Task.Factory.StartNew()` can also create and launch a Task in a single operation, and don't need to separate creation and scheduling, and/or additional state needs to be retreived from the `Task.AsyncState` property.

_Note_: Calling `Task.Result` property will ensure the async task will become _blocking_ while the caller waits for the Task to return if it is not in `Completed` state!

### TPL - Accessing Values From Lambda Tasks

- Lambda expressions allow access to variables that are in-scope of the outer-executing code block.
- _However_ if they are value-type, they will not get updated properly during the Parallel looping.
- Utilize `CustomData` to create new data instances so that refs are used during each iteration and the data will get updated as expected.
- Use `Task.AsyncState` property to access `CustomData` instances from within the delegate.

## TAP - Task Creation Options

Long running task expected? Use `new Task(() => MyLongRunningMethod(), TaskCreationOptions.LongRunning | TaskCreationOptions.PreferFairness);`.

Each thread has an associated `Thread.CurrentCulture` and `Thread.CurrentUICulture`. This affects formatting, parsing, sorting, and string comparison operations, and is used in resource lookups. The default setting is inherited from the Default System Culture. Threads launched by other Threads with specific Culture settings do _not_ inherit the parent Thread's setting.

## TAP - Creating Detached Child Tasks

Any Task created without specifying `AttachedToParent` will _not_ be synchronized with the parent Task in any way.

AKA 'Detached Nested Task' or 'Detached Child Task'.

The parent Task does _not_ wait for the detached child Task to finish (assume `Started` but not `Completed` nor `Faulted`).

The option `TaskCreationOptions.DenyChildAttach` prevents other Tasks from attaching to the configured (parent) task.

## TAP: Attaching State To A Task

Do _not_ inherit from `System.Threading.Tasks.Task` to do this.

_Do_ use `AsyncState` property to associate the data with the Task.

## Imperative and Declarative Programming

Imperative Programming: Directs teh control flow of the program.

- This is what I want.
- This is the order things need to run to get what I want.

Declarative Programming: Specifies logic and result without directing program flow.

- This is how to get what I want.

## References

[Parallel Programming](https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/) article on MSFT Learn.

[Data Structures for Parallel Programming](https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/data-structures-for-parallel-programming).

## Footer

Return to [Conted Index](./conted-index.html).

Return to [Root README](../README.html).
