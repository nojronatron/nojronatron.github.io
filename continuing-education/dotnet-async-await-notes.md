# Async-Await Learnings

Notes taken while working through [Stephen Cleary](https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/%5Carchive%5Cmsdn-magazine%5Cauthors%5CStephen_Cleary)'s March 2013 article [Async/Await - Best Practices in Asynchronous Programming](https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming).

## Overview

There are some basic rules of thumb to follow:

- Avoid async void
- Async all the way
- Configure context

These are a mix of good ideas, not necessarily hard-and-fast rules (at least not all of them).

## Avoid Async Void

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
- Event Handlers tend to have `private` access, which is also more difficult to test or use composition techniques.

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

## Avoid Mixing Synchronous and Asynchronous

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

## Configure Context

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

## Solutions To Common Async Problems

As written in _Async/Await Best Practices in Asynchronous Programming_:

- Create a task to execute code: `Task.Run` or `TaskFacotry.StartNet` but _not_ `Task ctor` nor `Task.Start()`.
- Create a teask wrapper for an operation or event: `TaskFactory.FromAsync` or `TaskCompletionSource<T>`.
- Support cancellation: `CancellationTokenSource` and `CancellationToken`.
- Report progress: `IProgress<T>` and `Progress<T>`.
- Handle streams of data: TPL Dataflow or Reactive Extensions.
- Synchronize access to a shared resource: `SemaphoreSlim`.
- Asynchronously initialize a reseource: `AsyncLazy<T>`.
- Async-ready producer/consumer structures: TPL Dataflow or `AsyncCollection<T>`.

## Other Things To Keep Top Of Mind

About using `ConfigureAwait` vs using just `await`:

- `ConfigureAwait()` only makes sense when _awaiting Tasks_.
- `await` acts _on anything awaitable_.
- Leaving these keywords makes reading (and understanding) the code simpler than searching for build/debug options or using additional keywords with other possible side-effects.

Controller Actions:

- They have their own Context.
- Actions called by Controllers _do not_ have their own Context.

## Resources

[Async/Await - Best Practices in Asynchronous Programming](https://learn.microsoft.com/en-us/archive/msdn-magazine/2013/march/async-await-best-practices-in-asynchronous-programming)

Stephen Cleary [adds a great response to a StackOverflow question](https://stackoverflow.com/questions/13489065/best-practice-to-call-configureawait-for-all-server-side-code) that is worth reviewing, especially in the context of (now legacy) ASP.NET.

Read more about the Task-based Asynchrounous Pattern [TAP in .NET: Introduction and overview on MSDN](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap?redirectedfrom=MSDN).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
