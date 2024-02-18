# Async-Await Learnings

Notes taken while working through [Stephen Cleary](https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/%5Carchive%5Cmsdn-magazine%5Cauthors%5CStephen_Cleary)'s March 2013 article [Async/Await - Best Practices in Asynchronous Programming](https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming).

Additional notes were taken while reading [Task-based Asynchronous Programming Patterns](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap) from learn.microsoft.com.

## Best Practices Reading Overview

There are some basic rules of thumb to follow:

- Avoid async void
- Async all the way
- Configure context

These are a mix of good ideas, not necessarily hard-and-fast rules, as there are details to each one depending on the DotNET version including ASP.NET, WinForms, WPF, etc.

## Best Practices - Avoid Async Void

Async methods can return any of these three types:

- Void (with limitations)
- Task
- Generic Task

Async Void should not be used _except_ in the case of asynchronous Event Handlers:

- WPF generates Async Void handlers for button-push events, etc.
- When an exception is thrown are raised directly on the `SynchronizationContext` that was active when the handler was called, so they cannot be caught easily.
- Implementing Async Void methods in _unmaintainable_ and _not recommended_.
- Cannot be composed using `Task.WhenAny` or `Task.WhanAll`.
- MSFT Unit Testing only support async `Task` and `Task<T>` methods.
- Event Handlers tend to have `private` access which is more difficult to test and to compose with other methods.

Async Task methods are preferred when there is no return Type expected:

- When an asynchronous method returns, it returns an empty (void) Task.
- Exceptions are captured and put into the Task object, so it is easier to catch and handle.
- The calling method _knows_ that a Task-returning method is asynchronous.

Generic Async Task methods provide the most capability:

- The return type will be encapsulated in the Task object, for ex: `Task<MyCustomObject>` returns a `MyCustomObject` instance.
- Exceptions are captured and put into the Task object, making it easier to catch and handle.
- Theh calling method _knows_ the `Task<T>`-return method is asynchronous.

```c#
public async void ChildMethodAsync()
{
  throw new InvalidOperationException();
}
public void ParentMethod()
{
  try
  {
    ChildMethodAsync();
  }
  catch (Exception)
  {
    // will not get caught!
    throw;
  }
}
```

In order to _see_ these Exceptions while debugging, use `AppDomain.UnhandledException` (commonly available in WPF, ASP.NET).

A better approach:

```c#
// WPF event handler
private async void MyButton_OnClick(object sender, EventArgs e)
{
  await MyCustomMethodAsync();
}

// apply async Task to the custom method
public async Task MyCustomMethodAsync()
{
  // do awaitable work etc
  await Task.Run(()=> ...);
}
```

This provides:

- Testability of MyCustomMethodAsync.
- Exception handling capability in MyCustomMethodAsync.
- Asynchronous task execution.
- Minimal added code-behind, especially the Event Handler simply calls an async method on an injected service instance.

### When Using Lambdas, Anonymous Methods, and Other Delgates

Do not "...provide an async implementation (or override) to a void-returning method on an interface (or base class)":

- Callers and Events might assume the method is complete when it returns.
- Passing-in an async lambda that returns void will produce the same issues as an _async void_ method!
- `Action<T>` returns void, and is the delegate form of a void lambda, and so will also inherit all the same _async void_ method issues.

"Lambdas should only be used if they're converted to a delegate type that returns Task (for example, `Func<Task>`)." To do this, encapsulate a void-return lambda expression in an `Action/<T>` delegate, similar to how a `delegate` can encapsulate a named method.

See [.net 8 Action\<T>](https://learn.microsoft.com/en-us/dotnet/api/system.action-1?view=net-8.0) for how to utilize `Action<T>` delegate.

## Best Practices - Avoid Mixing Synchronous and Asynchronous

There are consequences to doing this:

- Using blocking code in an Async method (use of `Task.Wait` or `Task.Result`).
- Deadlocks: The calling method in the "captured context" is on a blocking thread waiting for the blocked async method which is waiting for access to its "captured context" but the thread is blocked.

### Special Case: Console Applications

Thread Pool SynchronizationContext:

- Console Apps use this to enable scheduling threads itself.
- Other App types use a "one-chunk-at-a-tyime" `SynchronizationContext` that does _not_ allow thread selection outside of the calling "context".
- `Main` method _cannot by async_ else the Console App would complete before any code ran.

_Warning_: Moving asynchronous code from a Console Application to a GUI or ASP.NET application will require editing the code to avoid deadlocks.

### Adding Async Code to Existing Codebase

- Allow async code to grow naturally.
- Async code should expand from its entry point (e.g. Event Handlers or Controller actions).
- If a partial solution is necessary (on a temporary basis during conversion), weigh the possible benefit to the risks of possible deadlocks and Exception handling while using `Task.Wait` or `Task.Result`.

### Tasks Store Lists of Exceptions

When an Exception is thrown within an async (read: Task based) method:

- If awaited: The first Exception is re-thrown so it can be caught.
- If blocked via `Task.Wait` or `Task.Result`: Exceptions are wrapped in `AggregateException` and _then_ thrown.
- If try-catch block is in a non-async method, any awaited Task based Exception will be wrapped in `AggregateException` and must be "unwrapped" to get each Exception (even if there is only 1).
- If try-catch block is within a Task/Async method, the specific Exception can be handled or rethrown by name or generally with `Exception`.

### Blocking Within Async Method

Methods that "aren't fully asynchronous" will not return a completed Task.

Async code should not include synchronous, blocking code.

An example as written in _Async/Await Best Practices in Asynchronous Programming_

```c#
public static class NotFullyAsynchronousDemo
{
  // This method synchronously blocks a thread
  public static async Task TestNotFullyAsync()
  {
    // Yield is an immediate-return statement (an incomplete Task)
    await Task.Yield();
    // Upon returning the next line of code will block the GUI or ASP.NET request thread
    Thread.Sleep(5000);
  }
}
```

### The Async Way

To Retrieve the result of a background task: _Do not_ use `Task.Wait` or `Task.Result` and _instead_ use `await`

To Wait for any Task to complete: _Do not_ use `Task.WaitAny` and _instead_ use `await Task.WhenAny`

To Retrieve the results of multiple tasks: _Do not_ use `Task.WaitAll` and _instead_ use `await Task.WhenAll`

To Wait a period of time: _Do not_ use `Thread.Sleep` and _instead_ use `await Task.Delay`

## Best Practices - Configure Context

Context is captured when an incomplete Task is awaited.

Captured context is used to resume the async method.

Resuming on the Context causes performance problems (slight, but they accumulate).

_Advice_: Await teh result of ConfigureAwait whenever possible.

### ConfigureAwait

`ConfigureAwait(bool)` or `ConfigureAwait(ConfigureAwaitOptions)`

`ConfigureAwaitOptions`:

- An Enum of [configure await options](https://learn.microsoft.com/en-us/dotnet/api/system.threading.tasks.configureawaitoptions?view=net-8.0).
- ContinueOnCapturedContext: Marshal continuation back to original SynchronizationContext (or TaskScheduler) on calling thread when Task was awaited.
- ForceYielding: Forces `await` on already completed Task to behave as if Task is not yet completed (forcing a Yield).
- None: No options specified.
- SuppressThrowing: Avoids throwing Exception at completion of `await` of a Task that has ended in a Faulted or Canceled state.

ConfigureAwait best practices:

- Separates awaited Task Context and uses the Thread Pool instead.
- Calling context no longer pays attention to the awaited Task.
- Remaining code runs in the context of the Thread Pool (and not the GUI Thread or similar).
- This has performance improvements when used in GUI-based code.
- Calling a Component of the GUI from this `ConfigureAwait()` Task requires additional code.
- _Avoid using ConfigureAwait()_ when code _following the await_ needs to access the original context.
- Consider this a "Fire and Forget"!
- Async Methods calling other Async Methods generate independant Contexts.
- Context-free code is more reusable.
- Minimize code within Context-sensitive Event Handler.

## Best Practices - Solutions To Common Async Problems

As written in _Async/Await Best Practices in Asynchronous Programming_:

- Create a task to execute code: `Task.Run` or `TaskFacotry.StartNet` but _not_ `Task ctor` nor `Task.Start()`.
- Create a teask wrapper for an operation or event: `TaskFactory.FromAsync` or `TaskCompletionSource<T>`.
- Support cancellation: `CancellationTokenSource` and `CancellationToken`.
- Report progress: `IProgress<T>` and `Progress<T>`.
- Handle streams of data: TPL Dataflow or Reactive Extensions.
- Synchronize access to a shared resource: `SemaphoreSlim`.
- Asynchronously initialize a reseource: `AsyncLazy<T>`.
- Async-ready producer/consumer structures: TPL Dataflow or `AsyncCollection<T>`.

## Best Practices - Other Things To Keep Top Of Mind

About using `ConfigureAwait` vs using just `await`:

- `ConfigureAwait()` only makes sense when _awaiting Tasks_.
- `await` acts _on anything awaitable_.
- Leaving these keywords makes reading (and understanding) the code simpler than searching for build/debug options or using additional keywords with other possible side-effects.

Controller Actions:

- They have their own Context.
- Actions called by Controllers _do not_ have their own Context.

## TAP - Overview

This is a brain-dump of concepts and mid-level details from the Summary chapter:

- Method name suffix: Async or TaskAsyc (if former is taken) for awaitable Types.
- Awaitable Types: `Task`, `Task<TResult>`, `ValueTask`, `ValueTask<TResult>`.
- TAP Method doesn't return an awaitable type? Name prefix `Start` or `Begin` to imply that the method will not return or throw the result of the async operation.
- For void return, return a `Task`.
- For Type return, return a `Task<T>`.
- AVOID: `OUT` and `REF` keywords in arguments list. Use a `TResult` that is a `Tuple` or custom Type instead.
- Built-in Combinators: `WhenAll`, `WhenAny`.
- Minimize Synchronous work within an Async method and keep it at the START of the method.
- Fast-returning async Tasks could return a COMPLETED Task, acting much like a synchronous call.
- Usage error Exceptions should NEVER HAPPEN! Ensure all args to a TAP method are validated e.g. no Null inputs that wouldn't be handled.
- All other Exceptions that could occur within the Async Task should be encapsulated into the returning Task.
- TAP allows determining where asynchronous execution occurs: UI Thread, some other specific Thread, the Thread Pool, Async I/O, or some attached Context.
- Continuation Code: Code that runs after an asynchronous operation completes.
- Task object includes methods to run Continuation Code for e.g. `ContinueWith()` or the `await` keyword.
- TaskStatus: `Enum`, provides information on Task lifecycle.
- Tasks created via CTOR are "Cold" meaning they are non-scheduled and state is enum:Created but not running until `Task.Start()` is called on them.
- Tasks created ANY WAY OTHER THAN CTOR start hot, e.g. scheduled and enum state anything BUT enum:Started.
- Consumers (calling methods) should NEVER be in charge of calling `Task.Start()` and will always assume a return `Task` is in any state OTHER THAN enum:Created. Calling `Task.Start()` on a returned `Task` will cause `InvalidOperationException` to be thrown.
- Cancellation is OPTIONAL for both async Consumers and async implementers.
- If Async method accepts cancellation: Include an async method overload that includes `CancellationToken` argument.
- Aync operations should monitor `CancellationToken` instance for a cancellation request, and OPTIONALLY act on it to cancel its operation.
- Prematurely canceled Task should return a state of Canceled, without any available Result or Exception thrown.
- A Task state of Canceled is considered to be a FINAL STATE for a Task, just like `Faulted` and `RanToCompletion`.
- Tasks that are Canceled that were called using `Wait()` and `WaitAll()` will continue to run with an Exception.
- Progress reporting is OPTIONAL: Pass `IProgress<T>` as an async method parameter. Generally used to update UI with Task status info.
- Implementation of `Progress` is determined by the consuming code.
- `IProgress` implementation options include: Act upon only the latest update; Buffer all updates; Invoke an action at each update; Control whether update is marshalled to a particular Thread.
- `IProgress<T>` implementing methods MUST allow IProgress to be Null w/o throwing.
- `IProgres<T>` updates are SYNCHRONOUS (so that they are immediately reported).
- `IProgress<T>` could utilize a Tuple with data such as: double:percentComplete, `List<string>`:filesDiscovered; A Custom Type (suffix 'ProgressInfo') that encapsulates the API definition of progress.
- `IProgress<T>` CTOR allows providing a single Event Handler, or MULTIPLE Event Handlers can be subscribed via the `ProgressChanged` property.
- When providing Cancellation and Progress capabilities, be sure to provide overloaded async Task methods but usually neither are included which simplifies the params list.
- If both `IProgress<T>` and `CancellationToken` params are availabe in the async method, then up to 3 added overloads will be required beyond the base params list: MyMethodAsync(obj myParam); MyMethodAsync(CancellationToken cn, obj myParam); MyMethodAsync(`IProgress<T>` progress, obj myParam); MyMethodAsync(CancellationToken cn, `IProgress<T>` progress, obj myParam);
- Defaults of`CancellationToken`= None and `IProgress<T>` = null can be used to reduce total overloads to only two.

## TAP - Generating Methods

Generating TAP Methods can be done three ways:

1) Compiler: Use the 'async' keyword and returning a `System.Threading.Tasks.Task` or ...`Task<TResult>`. Exceptions are packaged in the Task object and TaskStatus.Faulted state is set. `OperationCanceledException` that are UNHANDLED results in TResult Task.Canceled state.
2) Manually: Provides better control over implementation. Use `System.Threading.Tasks` and `System.Runtime.CompilerService` namespaces. Create a `TaskCompletionSource<TResult>` object that calls SetResult when completed, or SetException when faulted, or SetCanceled if canceled by token (TrySetException, TrySetException, and TrySetCanceled, accordingly).
3) Hybrid: Implement TAP pattern manually but delegate core logic to the compiler. Use this to validate arguments and catch Exceptions outside of the Compiler-generated async Task implementation. In essence: Ensure Exceptions are thrown back to the calling function, rather than wrapped in a `System.Threading.Tasks.Task` object. This pattern can also be used to "return a cached Task".

Example MANUAL generation of a TAP method:

```c#
// Manually generating a TAP method
public static Task<int> ReadTask(this Stream stream, byte[] buffer, int offset, int count, object state)
{
  // Quote: When you implement a TAP method manually
  // you must complete the resulting task when the
  // represented asynchronous operation completes.
    var tcs = new TaskCompletionSource<int>();
    stream.BeginRead(buffer, offset, count, ar =>
    {
        try 
    { 
      tcs.SetResult(stream.EndRead(ar)); 
    }
        catch (Exception exc) 
    { 
      tcs.SetException(exc); 
    }
    }, state);
    return tcs.Task;
}
```

Example HYBRID TAP method generation:

```c#
// Hybrid TAP method generation
public Task<int> MethodAsync(string input)
{
    if (input == null) throw new ArgumentNullException("input");
    return MethodAsyncInternal(input);
}

private async Task<int> MethodAsyncInternal(string input)
{
   // code that uses await goes here
   return value;
}
```

## TAP - IO and Compute Workloads

### IO Workloads

Includes asynchronous methods that are awaiting (a usually remote) process to return results, but not utilizing compute.

Ensure these are set to be asynchronous:

- Should not back these with a Thread for the entirety of execution!
- Use`TaskCompletionSource<TResult>`type, which exposes Task property  that returns`Task<TResult>`instance.
- Task lifecycle will lbe managed by`TaskCompletionSource<TResult>`methods: `SetResult()`, `SetException()`, `SetCanceled()` and their 'TrySet' variants.

### Compute Workloads

Includes asynchronous methods that are performing the computationally heavy processing.

Although these shouldn't be exposed publicly from the library, if they are they should be exposed as Synchronous (NOT async).

The implementation Library can decide whether to offload them to another thread or execute them in parallel.

### Common Compute and IO Implementations

`Task.Run()` and `TaskFactory.StartNew()`:

- Former is shortcut for the latter.
- Easily launch compute-bound task targeting the thread pool.
- `TaskFactory.StartNew()`() is well suited for fine-grained control over a Task with `CancellationToken`, `TaskCreationOptions`, and `TaskScheduler` params list overloads.
- Create a new Task in a private method using `TaskFactory`, then `Start()` the Task separately if needed.
- "Public methods must only return tasks that have already been started."

`Task.ContinueWith()`:

- Creates new Task that is scheduled when another Task completes.
- Some overloads allow supplying `CancellationToken`, continuation options, and a TaskScheduler.

`TaskFactory.ContinueWhenAll()` and `TaskFactory.ContinueWhenAny()`:

- Both will create new Task, scheduled for when all (or any) of supplied Task(s) completes.
- Overloads provide for scheduling and execution of these tasks.

In a Compute-bound Task:

- Accept a `CancellationToken` in the params list.
- Poll the `CancellationToken` within the body of the method using `token.ThrowIfCancellationRequested()`.
- If unhandled, the Task will return in the state of `Canceled`.
- If other unhandled Exceptions are thrown, the Task will end in the state of `Faulted`.

Hybrid Workloads: Compute-bound and IO-bound:

- Utilize a single `CancellationToken` so if IO-bound task returns `Cancelled`, following Task(s) are also returned in `Cancelled` state.

## TAP - Consuming TAP

- Can use Callbacks to wait without blocking by using `Task.ContinueWith()`.
- Allows async ops within normal control flow and compiler-generated code.
- await `Task`: Returns void; await `Task<TResult>`: returns TResult.
- Await actually installs a Callback on the `Task` by using "continuation".
- The callback resumes async method where it was suspended.
- When async method is resumed: The Tasks `TResult` is returned (if operation completed successfully). Canceled? `OperationCanceledException` is thrown. Faulted state? Exception that caused the fault is re-thrown.
- When `Faulted`: Only a single Exception is propagated: `AggregateException`, containing all actually thrown `Exceptions`.

If `SynchronizationContext` object is associated with thread that executed async method when suspended:

- If `SynchronizationContext.Current` property is not null: async method resumes in same context using context's `Post()` method. Null? Relies on `TaskScheduler` object that was current when method was suspended (usually the default `TaskScheduler` on the Thread Pool). Resumption could be executed or scheduled.
- Async methods synchronously execute body code until the first await expression that has not yet been completed. Invocation is then returned to the calling function.
- A return statement causes an async method to return a `Task` in state `RanToCompletion`.

Configure Suspend/Resume with `Yield` and `ConfigureAwait`:

- `Task.Yield()`: Equivalent to asynchronously posting or scheduling back to the current Context.
- `Task.ConfigureAwait()`: Current Context is captured when async method is suspended. This is used to invoke async method continuation point when resumed. Inform the await operation to NOT capture and resume on Context and instead continue wherever the async operation that was being awaited completed.

```c#
// do not use this if it is important to return
// to a specific context like the UI thread
await someTask.ConfigureAwait(continueOnCapturedContext:false);
```

## TAP - Canceling Async Operations

Canceling Async Operation:

- Use `CancellationTokenSource` to generate a `CancellationToken` i.e. `ConcellationTokenSource.Token`.
- The source calls `Cancel()` to signal the `CancellationToken`.
- One token can cancel multiple async invocations.
- `Cancellation` can be requested FROM ANY THREAD.
- `Cancellation.None` means "Can not be canceled by Token".

_Note_: It is also possible for a Task to "self cancel" by calling the passed-in `CancellationToken` and calling its `Cancel()` method!

## TAP - Monitoring Async Operation Progress

Monitoring Progress:

- Pass-in Progress inidating interface to async methods.
- There is a simple WPF example in the text (see below).

```c#
// consume this method by WPF to track download
// progress initiated by a button event handler
private async void btnDownload_Click(object sender, RoutedEventArgs e)
{
    btnDownload.IsEnabled = false;
    try
    {
        txtResult.Text = await DownloadStringTaskAsync(txtUrl.Text,
            new Progress<int>(p => pbDownloadProgress.Value = p));
    }
    finally { btnDownload.IsEnabled = true; }
}
```

## TAP - Combinators

Built-in Task-based Combinators:

- `Task.Run(Func<Task>())`: Shorthand for `TaskFactory.StartNew()`. Good for offloading async work.
- `Task.FromResult(arg)`: Use when data may already be available and just needs to be returned within a `Task<TResult>`.
- `Task.WhenAll()`: Wait on multiple async operations represented by `Task` or `TResult`. Multiple Overloads are available. Applies Paralellism to each started `Task`. Exceptions propagate out of each Task and can be caught specifically (rather than by an `AggregateException` object).
- `Task.WhenAny()`: Await any single Task-based operation for Redundancy (compare 1st completion to others), Interleaving (process each completion _as they complete_), Throttling (Allow other Tasks to start as others complete - an extension of Interleaving), or Early Bailout (As soon as one task returns a cancellation or other 'signal', other incomplete Tasks get cancelled before completing).

### About Task WhenAll

If a `try-catch` block wraps an `await Task.WhenAll()` operation, the Exceptions _are_ consolidated into `AggregateException`.

Unwrap `AggregateException` by performing a `foreach` in the catch block and iterate through `Task` items selecting by `Task.IsFaulted` and capture each Task Exception using `Task.Exception` property.

### About Task Delay

Introduce pauses into async method execution:

- Build polling loops.
- Delay handling on user input.
- Set timeouts on awaits while calling `Task.WhenAny()`.
- Use `try` to capture `WhenAny()` or `WhenAll()` execution and a `finally` bock to ensure any continuation code is executed.

Caveats:

- Operation execution could suffer if a Task fails to complete.
- Developer should include a timeout period while waiting on async ops.
- `TaskFactory.ContinueWhenAll` and `TaskFactory.ContinueWhenAny()` do _not_ accept timeouts!
- Synchronous `Task.Wait()`, `Task.WaitAll()`, and `Task.WaitAny()` accept timeouts.
- Leverage `Task.Delay()` and `Task.WhenAny()` to implement a timeout.

## TAP - Building Task-based Combinators

Several Combinators are included in the .NET Libraries, but custom Combinators can be designed and implemented:

- Synchronous: `RetryOnFault<T>(Func, maxRetries)`
- Async: Same as synchronous but returns a `Task<T>`, accepts a `Task<T>`, and calls `return await function().ConfigureAwait(false)`

In either of the examples in subsection [RetryOnDefault](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern#retryonfault), the custom methods attempt to return a function (awaited function using TAP) that might throw. A `catch` statement tests the number of times the attempt has been made (1 to maxRetries) and will `throw` on the last retry, else will iterate until last retry then return `default(t)`.

Other ideas include:

- Adding a timeout/retry for one or more Tasks.
- Calling a `Func<Task>` between retries to determine when to retry.

### Custom Combinator Example: NeedOnlyOne

If calling multiple APIs but a response from only 1 is needed, pick the 1st one to return and cancel the remaining calls, and return only the 1st completed call.

Overview (see the actual page for the code):

1. Accept a `Func<T>` as an array of Cancellation Token and `Task<T>` instances (`[] functions`).
2. Iterate through each `function` in `functions` and assign them to new `Task[]` array.
3. Call `await Task.WhenAny(collectionOfFunctionInstances).ConfigureAwait(false)` and assign the result to a variable e.g. `completed`.
4. Call `cancellationToken.Cancel`.
5. Iterate through each `Task` in tasks array and implement `TaskContinuationOptions.OnlyOnFaulted`, assigning them to a variable e.g. `ignored`.
6. Return `completed` variable (which is a `Task`).

### Custom Combinator Example: Interleaved Operations

`WhenAny()` might introduce performance problems because it registers a Continuation with each Task.

Following a technique as explained in [Interleaved Operations](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern#interleaved-operations) can help to avoid issues with performance and handling completed and/or failed tasks.

_Note_: Thread safety is important here and using the [Interlocked](https://learn.microsoft.com/en-us/dotnet/api/system.threading.interlocked?view=net-8.0) class might be necessary to avoid preemptive overwriting of an instance variable (for example).

Another possible custom Combinator is `Task<T> WhenAllOrFirstException(IEnumerable<Task<T>>)`:

- Wait for all tasks in a set.
- UNLESS one of them faults then stop waiting.

## Building Task-Based Data Structures

Leverage `Task` and `Task<TResult>` with data structures in an async-compatible way.

AsyncCache:

- Task might be handed out to multiple consumers.
- Consumers may await the same task.
- Consumers may register Continuations with the same task.
- Consumers may get results or Exceptions from the same task.

The article demonstrates a custom Class of type `TKey, TValue` (a dictionary or KVP), where an internal `ConcurrentDictionary<Tkey, Lazy<Task<TValue>>>` maintains values registered via the CTOR, and accessed using an `indexer` method. Accepting a `Func<TKey, Task<TValue>> valueFactory` delegate ensures previously-added KVPs are rapidly found and a cahced copy can be returned using `key`. Since this is built on top of `System.Threading.Tasks.Task` it is capable of handling concurrent operations (multiple key access).

The [Async Producer Consumer Collection](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern#asyncproducerconsumercollection):

- Coordinate async activities.
- Producers generate data.
- Consumers consume data from Producers.
- Producers and Consumers can run in parallel.
- Consumers are _notified_ by a Producer when a Producer has new data available.

An example as written in the _Asunc Producer Consumer Collection_ (linked above):

```c#
public class AsyncProducerConsumerCollection<T>
{
    private readonly Queue<T> m_collection = new Queue<T>();
    private readonly Queue<TaskCompletionSource<T>> m_waiting =
        new Queue<TaskCompletionSource<T>>();

    public void Add(T item)
    {
        TaskCompletionSource<T> tcs = null;
        lock (m_collection)
        {
            if (m_waiting.Count > 0) tcs = m_waiting.Dequeue();
            else m_collection.Enqueue(item);
        }
        if (tcs != null) tcs.TrySetResult(item);
    }

    public Task<T> Take()
    {
        lock (m_collection)
        {
            if (m_collection.Count > 0)
            {
                return Task.FromResult(m_collection.Dequeue());
            }
            else
            {
                var tcs = new TaskCompletionSource<T>();
                m_waiting.Enqueue(tcs);
                return tcs.Task;
            }
        }
    }
}
```

Now leverage the above code:

```c#
private static AsyncProducerConsumerCollection<int> m_data = …;

// additional fields, properties

private static async Task ConsumerAsync()
{
    while(true)
    {
        int nextItem = await m_data.Take();
        ProcessNextItem(nextItem);
    }
}

// additional members

private static void Produce(int data)
{
    m_data.Add(data);
}
```

With `BufferBlock<T>`:

```c#
private static BufferBlock<int> m_data = ; // some value

// other fields and props...

private static async Task ConsumerAsync()
{
    while(true)
    {
        int nextItem = await m_data.ReceiveAsync();
        ProcessNextItem(nextItem);
    }
}

// other members here

private static void Produce(int data)
{
    m_data.Post(data);
}
```

## Things To Review

If cancellation is requested but a result or an exception is still produced, the task should end in the `RanToCompletion` or `Faulted` state.

A TAP method may even have nothing to execute, and may just return a Task that represents the occurrence of a condition elsewhere in the system (for example, a task that represents data arriving at a queued data structure).

The Producer-Consumer Collection pattern!

NuGet Package [System.Threading.Tasks.Dataflow](https://www.nuget.org/packages/System.Threading.Tasks.Dataflow).

## Resources

[Async/Await - Best Practices in Asynchronous Programming](https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming)

Stephen Cleary [adds a great response to a StackOverflow question](https://stackoverflow.com/questions/13489065/best-practice-to-call-configureawait-for-all-server-side-code) that is worth reviewing, especially in the context of (now legacy) ASP.NET.

Read more about the Task-based Asynchrounous Pattern [TAP in .NET: Introduction and overview on MSDN](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap?redirectedfrom=MSDN).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
