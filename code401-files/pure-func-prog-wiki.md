# Pure Functional Programming

Read the Wikipedia article about PFP and write about what I learned.

## Resource

Wikipedia article on [Purely Functional Programming](https://en.wikipedia.org/wiki/Purely_functional_programming)

## Notes and Comments

Is a programming paradigm.

State-transform functions are the computational processors.

State is input as a parameter to the functions.

Functions return an updated state when its computations have completed.

Purely Functional designs depend solely on their input, not any local or global state, to do their processing.

"Impure" Functional Programming is arguably similar or different than "Pure" Functional Programming and it is a subjective topic.

Arrays and methods that use *mutable cells* natively "update their state as side effects". *[Wikipedia article, accessed 9-June-22]*

Data Structures can be purely functional => This is known as persistence, an aspect of functional programming.

Functional Programming states that a given input will *always* result in the same output regardless of other contexts.

If a 5 is input into a purely functional method, then a 10 could be expected as output if the processing section was `return input * 2`, and it would not matter what temperature it was inside, what other data or 'state' there was around that function, it simply did *one thing* and *only one thing*.

### Eager and Lazy Stuff

Eager Evaluation and Lazy Evaluation are ways of describing when functions (or operations) are executed.

It is difficult to know exactly when lazy operations will actually execute, and could even be *after* the defining function has returned and exited.

Eager evaluations are always executed immediately, so ordering them in a specific way could impact their results, making the mixture of them less-than-purely-functional methods.

Lazy evaluations mixed with eager ones makes prediction of outcome even more difficult.

Lazey evaluations on their own are easier to implement because their outputs can be delayed in a predictable (and sometimes controllable) way.

### Parallel Computing

Using purely functional programming is preferred with synchronous or parallel execution environments because outputs can be predicted regardless of what order the functions are processed.

### A Note About Imperitive Programming

Uses statements that change the state of a program.

Describes *how* a program operates.

It a step-by-step methodology.

Cantrast with declarative programming: *What* the program should accomplish, sans details of *how* results are achieved.

Procedural programming is similar to declarative, although the program as a whole still identifies many steps determining *how* the end result is made.

## Footer

Back to root [README](../README.md)
