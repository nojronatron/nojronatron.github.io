# DotNET Task Parallel Library Notes

Notes taken while reviewing MSFT Learn documentation of Task Parallel Library (TPL).

## Table of Contents

- [Overview](#overview)
- [Reminder: Imperative and Declarative Programming](#reminder-imperative-and-declarative-programming)
- [TPL - Task Parallel Library](#tpl---task-parallel-library)
- [TPL - For and ForEach](#tpl---for-and-foreach)
- [TPL - Create And Run Tasks Implicitly](#tpl---create-and-run-tasks-implicitly)
- [TPL: Potential Pitfalls](#tpl-potential-pitfalls)
- [TPL - Concurrent Collections](#tpl---concurrent-collections)
- [TAP - Task Creation Options](#tap---task-creation-options)
- [TAP - Creating Detached Child Tasks](#tap---creating-detached-child-tasks)
- [TAP Attaching State To A Task](#tap-attaching-state-to-a-task)
- [PLINQ - Overview](#plinq---overview)
- [PLINQ - ParallelEnumerable Class](#plinq---parallelenumerable-class)
- [PLINQ - Behaviors Overview](#plinq---behaviors-overview)
- [PLINQ - Measuring Performance](#plinq---measuring-performance)
- [References](#references)
- [Footer](#footer)

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

## Reminder: Imperative and Declarative Programming

Imperative Programming: Directs teh control flow of the program.

- This is what I want.
- This is the order things need to run to get what I want.

Declarative Programming: Specifies logic and result without directing program flow.

- This is how to get what I want.

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

## TPL: Potential Pitfalls

- TAP is not always faster than other patterns. Always measure actual results to know how your code performs with, and without, TAP.
- Avoid writing to shared memory locations, this will cause race conditions. This includes writing to static variables or class fields. Instead, write `Parallel.For` and `Parallel.ForEach` using `System.Threading.ThreadLocal<T>` variable to store data during execution.
- Avoid over-parallelizing. The cost of partitioning the data before operating on it can cost more than using other techniques to iterate over a data structure.
- Avoid nested loops, as this is a common cause of over-parallizing. Stick with parallizing just the outer loop. There are exceptions but this is a good rule-of-thumb.
- Avoid calling Non-Thread-Safe methods. This can lead to data corruption, and/or throw Exceptions.
- Limit calls to Thread-Safe methods. Most DotNET methods are thread-safe and can be called by multiple threads concurrently, but there is a cost to synchronizing these calls.
- Thread Affinity restrictions exists in COM for STA components, Windows Forms, and WPF. This requires code to run on a specific thread e.g. the UI thread for WPF.
- Waiting in Delegates that are called by `Parallel.Invoke` _might_ cause a deadlock. Specify a timeout on `Wait` operations to ensure one Task cannot block another.
- TPL iterative Tasks are _not guaranteed to run in parallel_.
- Starvation of Threads can lead to deadlocks. This is where a single Task thread is started, and awaited by many other threads. If any awaiting Thread blocks the initial Task thread, the initial Task thread will never complete, and all awaiting Task threads will wait forever.
- Avoid executing Parallel Loops on the UI Thread. Running Parallel Loops on the UI thread will block the UI thread, causing delays in the user interface. This is also related to Thread Affinity restrictions, but not entirely the same. Use Marshalling to grab the update/result to push it to the UI thread.

## TPL - Concurrent Collections

Namespace `System.Collection.Concurrent`.

Provide thread-safe `Add()` and `Remove()` methods.

Avoids locks.

Leverages fine-grained locking when necessary.

User code does _not_ need to explicitly take locks to get these to work.

Multiple threads can add and remove items from these collections.

### Existing Concurrent Collection Classes

`System.Collection.Concurrent.BlockingCollection<T>`:

- Blocking and bounding capable thread-safe collections.
- [BlockingCollection (.NET 6)](https://learn.microsoft.com/en-us/dotnet/api/system.collections.concurrent.blockingcollection-1?view=net-6.0).

`System.Collections.Concurrent.ConcurrentBag<T>`:

- Thread-safe bag implementation for scalable add and get operations.
- [ConcurrentBag (.NET 6)](https://learn.microsoft.com/en-us/dotnet/api/system.collections.concurrent.concurrentbag-1?view=net-6.0).

`System.Collections.Concurrent.ConcurrentDictionary<TKey,TValue>`:

- Generic Dictionary class.
- Thread-safe and concurrent-aware.
- [ConcurrentDictionary (.NET 6)](https://learn.microsoft.com/en-us/dotnet/api/system.collections.concurrent.concurrentdictionary-2?view=net-6.0).

`System.Collection.Concurrent.ConcurrentQueue<T>`:

- Generic FIFO Queue class.
- Thread-safe, concurrent-aware.
- Uses Interlocked operations.
- [ConcurrentQueue (.NET 6)](https://learn.microsoft.com/en-us/dotnet/api/system.collections.concurrent.concurrentqueue-1?view=net-6.0).

`System.Collections.Concurrent.ConcurrentStack<T>`:

- Generic LIFO Stack class.
- Thread-safe, concurrent-aware.
- Uses Interlocked operations.
- [ConcurrentStack (.NET 6)](https://learn.microsoft.com/en-us/dotnet/api/system.collections.concurrent.concurrentstack-1?view=net-6.0).

`System.Collection.Concurrent.IProducerConsumerCollection<T>`:

- Manipulate thread-safe collections for "Producer-Consumer" usage.
- Use as an underlying storage mechanism for `Blocking Collection<T>`.
- Methods: CopyTo, ToArray, TryAdd, TryTake.

[Thread Safe Collections](https://learn.microsoft.com/en-us/dotnet/standard/collections/thread-safe/).

## TAP - Task Creation Options

Long running task expected? Use `new Task(() => MyLongRunningMethod(), TaskCreationOptions.LongRunning | TaskCreationOptions.PreferFairness);`.

Each thread has an associated `Thread.CurrentCulture` and `Thread.CurrentUICulture`. This affects formatting, parsing, sorting, and string comparison operations, and is used in resource lookups. The default setting is inherited from the Default System Culture. Threads launched by other Threads with specific Culture settings do _not_ inherit the parent Thread's setting.

## TAP - Creating Detached Child Tasks

Any Task created without specifying `AttachedToParent` will _not_ be synchronized with the parent Task in any way.

AKA 'Detached Nested Task' or 'Detached Child Task'.

The parent Task does _not_ wait for the detached child Task to finish (assume `Started` but not `Completed` nor `Faulted`).

The option `TaskCreationOptions.DenyChildAttach` prevents other Tasks from attaching to the configured (parent) task.

## TAP Attaching State To A Task

Do _not_ inherit from `System.Threading.Tasks.Task` to do this.

_Do_ use `AsyncState` property to associate the data with the Task.

## PLINQ - Overview

A paralell implementation on LINQ (Language-integrated Query).

- Implements standard LINQ query operators as extension metods.
- Adds operators for TPL (parallel operations).
- Operate on in-memory `IEnumerable` or `IEnumerable<T>` data sources.
- Do not execute until the query is enumerated.
- Data is partitioned (because it relies on TPL under the hood).

## PLINQ - ParallelEnumerable Class

Class `System.Linq.ParallelEnumerable`.

- Gets compiled into `Syste.Core.dll` assembly.
- Includes implementation of standard LINQ to Objects operators.
- Parallelization is not guaranteed.

Opt-in to TPL by invoking `ParallelEnumerable.AsParallel` extension method on the data source.

```c#
// example from Parallel LINQ (PLINQ) documentation on Learn.Microsoft.com
// in subsection "The Opt-in Model"
var source = Enumerable.Range(1, 10000);

// opt-in using AsParallel
var evenNums = from num in source.AsParallel()
               where num % 2 == 0
               select num;

Console.WriteLine("{0} even numbers out of {1} total",
                  evenNums.Count(), source.Count());

// expected output: 5000 even numbers out of 10000 total
```

## PLINQ - Behaviors Overview

PLINQ is conservative and will pick safety over speed, and LINQ over PLINQ if parallel operation appears to be expensive compared to sequential execution.

PLINQ will try to use all processors on the host PC. This can be limited to 'no more than n' using `WithDegreeOfParallelism(n)`.

`AsOrdered()` might still operate in Parallel but will maintain the sorting order rules on the source iterable. This will be slower than `AsUnordered()`.

PLINQ will run sequential queries when specific operations require it. Use `AsSequential()` to ensure sequential operation on the PLINQ operation.

PLINQ can be configured to mix sequential and parallel processing.

`ParallelMergeOptions` enumeration is used to tell PLINQ _how_ to merge results from each Thread back into the main thread result variable.

Execution is deferred until a query is enumerated _unless_ a method like `ToList()`, `ToArray()`, or `ToDictionary` are used.

Cancellation is supported by PLINQ by using `WithCancellation(CancellationToken token)`. Setting token to true will cause the PLINQ to cancel execution _on all threads_ and throw `OperationCanceledException`. _Note_: Remaining thread in-execution will run to completion!

PLINQ uses `AggregateException` to capture Exceptions thrown on threads other than the querying thread. Use a single `try-catch` block and capture `AggregateException` just like when using TPL and TAP.

Custom Partitioners can be written for PLINQ., and instantiated with the item source, then executed with `AsParallel().Select(func<T>)` etc.

## PLINQ - Measuring Performance

Overhead of setting up partitioning might not be worth running the work in parallel, so it could be executed sequentially.

Use [Parallel Performance Analyzer](https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/how-to-measure-plinq-query-performance) in Visual Studio Team Server (ed: HA!) to compare query performance, locate bottlenecks.

Also checkout [Concurrency Visualizer](https://learn.microsoft.com/en-us/visualstudio/profiling/concurrency-visualizer).

## References

[Parallel Programming](https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/) article on MSFT Learn.

[Data Structures for Parallel Programming](https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/data-structures-for-parallel-programming).

## Footer

Return to [Conted Index](./conted-index.html).

Return to [Root README](../README.html).
