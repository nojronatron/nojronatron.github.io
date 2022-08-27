# Time Complexity and BigO Notation

## Summary

Presenter: Isaiah Burkes

- US Army vet
- CS from Auburn University
- Python 401 Code Fellows (tested-in)
- SWE Intern at NASA
- SWE at MSFT currently

## Algorithmic Efficiency

We want to write efficient code.

Two types of efficiency measurements:

1. Time
1. Space

There are other costs.

Execution time: The number of operations multiplied by the time to execute each operation.

But specific measurements are not always necessary (or helpful).

Better: How does the run time of my code grow as the size of the input grows?

Time complexity will be the focus of this presentation.

## Big O Notation

Is not mathematically rigorous.

Helpful to figure out a functions uppper bounds.

Is a simplified means to communicate the complexity of an algorithm is terms of time to execute code vs the size of the input.

Logarithms:

- P is said to be the logarithm of the number n
- b^p = n
- 2^3 = 8
- n(log(b)) = p
- 8(log(2)) = 3

For algorithmic analysis, use base-2.

Helpful Question in sorting out logarithms: How many times do I have to divide by 2 until this number is equal to 1?

## Rules to Remember for Big O

1. Drop constants (a 1)
1. Different steps get added (addition)
1. Nested steps are multiplicative (multiply)
1. Different inputs get different variables
1. Drop non-dominant terms: n^2 is more dominant than 2n and n

## Code Examples

Coded in Python.

- O(1) => Constant => Code takes the same amount of time to process the input regardless of how large the input is.
- O(n + m) => A pair of iterators, one runs after another using different inputs.
- O(log(n)) => Regularly dividing inputs over and over again.
- O(n*m) => Nested loops, each depending on different inputs.
- O(n^2) => Nested loops, operating on the same input.

## Footer

Return to [Root README](../README.html)
