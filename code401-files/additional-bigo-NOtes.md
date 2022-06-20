# A BigO Notation Refresher

YouTube: [Ultimate Big O Notation Tutorial](https://www.youtube.com/watch?v=waPQP2TDOGE&ab_channel=BackToBackSWE)

## Back to Back SWE Notes

Upper Bounds: Not going to go past (some thing/gauge) as inputs become very large.

Root Concept: Ask yourself how does an Algo's speed scale when input becomes *very large*.

Look at the behavior of the graph as the input becomes very large.

Ask yourself "What is 'n'"? What are the variables? What is the *input*? Must know in order to derive BigO.

Multiple inputs of Strings? Then be sure to analyze those strings since they have *length of chars* so must evaluate *worst case* which would be Max(n, m) derived.

Constant Time: O(1) => As algo gets very large input, runtime stays the same.

Tail Behavior: How something scales. Constant-time means tail behavior is *straight*.

Logarithmic Time: O(log(n)) => Tail Behavior looks like a logarithmic graph. What do I need to "power 2 by" to "get to n"?

Binary Search: An inveriant means something is sorted in an expected way.

Balanced BST: Halves the search-space at every step along the way.

Unbalanced: *Must* visit *every node* in a search.

BigO: Always *drop the constants* because we only care about the *behavior*. A steep *line* is still a constant, it's just steep.

Quicksort and Mergesort BigO analysis: `O(n * log(n))` => Cutting things in half causes a Logarithmic count of n-levels in the *steps* of the algorithm. There is contant work being done within the Log(n) levels.

Bubble and Insertion Sort: O(n^2) => n by n steps then halved. Triangular numbers all end up being n^2 because constants are dropped.

Recursive and Backtracking algorithms: O(2^n) => Exponential Time.

Factorial Time: O(n!) => Algorithm that works through factorials. Remember: `3 * 2 * 1 = 3!`

### Optimizing

Less time? Uses more space.

Less space used? More time to complete.

Since time cannot be purchased, use more space rather than time => You can always buy more servers.

Space Complexity: How does the algorithm deal when inputs become very large?

Constant Time & Linear Space => Ask the question "Will stack space be included when evaluating this complexity?"

### Advice

Do not try to memorize the shape of code, you need to *know* what is actually going on.

If `log(n)`? Binary search!

## Kyle Talks About BigO

Web Dev Simplified Algorithms: [Learn Big O Notation in 12 Minutes](https://www.youtube.com/watch?v=itn09C2ZB9Y&ab_channel=WebDevSimplified)

### BigO Is Built Around

Thoughts about speed and how long does algorithm take as inputs get larger?

Thoughts about space and how much space will algorithm consume as inputs get larger?

What is the *core portion* of your algorithm?

How many times does the core of your algorithm execute, based on how many inputs there are?



## Footer

Return to [Root README](../README.html)
