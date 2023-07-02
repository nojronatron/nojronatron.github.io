# DSA Notes

Page dedicated to storing randome notes and thoughts about various data structures and algorithms.

Goal is to have a reference to path experiences with DSAs.

## Table of Contents

- [Quicksort](#quicksort)
- [DSA Key Takeaways](#dsa-key-takeaways)
- [Resources](#resources)
- [Footer](#footer)

## Quicksort

This kept me busy for a long time. Several attempts to solve this without looking directly at a solution were difficult experiences. There were times when I got close, and a few common issues would crop up:

- I hadn't set the correct stopping rules for recursive or iterative operations. After nearly sorting a sub-array, the algorithm would start _un-sorting_ the array.
- Arrays with duplicate items would not get sorted properly.
- Performance was _terrible_ compared to other sorting algorithms. Quicksort may not be the best for every scenario but many libraries utilize Quicksort at least in part.

### Quicksort References

I used the following references to get started with Quicksort:

Wikipedia: The article does a fair job of describing Quicksort and even has a neat animation supporting the descriptive text.

Essential Algorithms _[Stephens, Rod]_: The text does a fair job of describing Quicksort, but the pseudocode is actually mixed text and pseudocode which caused some confusion for me. Stephens reviews several approaches to finding a 'pivot'. He also discusses two methods to managing item swapping/replacement: Using Stacks or Recursion.

### Essential Algorithms Quicksort Code

Java:

```java
public class StephensQuicksort {
  public static void quicksort(int[] inputArr){
  if (inputArr.length < 2) {
    return;
  }
  int leftIdx = 0;
  int rightIdx = inptuArr.length - 1;
  quickSorter(leftIdx, rightIdx, inputArr);
  return;
  }

  public static void quickSorter(int start, int end, int[] numberArray){
    if (start >= end){
      return;
    }
    int divider = numberArray[start];
    int lo = start;
    int hi = end;
    boolean outerContinue = true;

    // find a value lower than divider and store its index
    while (true && outerContinue) {
      hi--;
      if (hi <= lo) {
        keepGoing = false;
      }
    }

    // if index of higher value has crossed the other index
    // place divider at that index but keep the hi index
    if (hi <= lo) {
      numberArray[lo] = divider;
      outerContinue = false;
      break;
    }

    // swap value at lower index with one in higher index
    // and move the index pointer forward for more testing
    numberArray[lo] = numberArray[hi];
    lo++;
    keepGoing = true;

    // find a value higher than divider and store its index
    while (numberArray[lo] < divider && keepGoing) {
      lo++;
      if (lo >= hi) {
        keepGoing = false;
        break;
      }
    }

    keepGoing = true;

    // reset lower index to higher index value and set
    // divider to higher index if the indices have crossed
    if (lo >= hi && outerContinue) {
      lo = hi;
      numberArray[hi] = divider;
      outerContinue = false;
      break;
    }

    // reassign array at hi index with
    // value from array at low index
    numberArray[hi] = numberArray[lo];
  }

  // partition: only send array element from start
  // to wherever low index is now (exclusive)
  quickSorter(start, lo - 1, numberArray);

  // only send array elements above through end of
  // array to the recursive call for next sort run
  quickSorter(lo + 1, end, numberArray);

  // if code reaches this point this function get removed from
  // the stack and calling function continues where it left off
  return;
}
```

## DSA Key Takeaways

1. While developing pseudocode, just write-out all the steps to get the job done. Writing pseudocode that is separated into functions and performs anything more than the necessary catches and data tests takes too long and the problem space is harder to solve.
2. Once pseudocode is passing a few smoke tests (including a Golden Path test), write actual code per pseudocode and debug it as a single file in the IDE.
3. If wanted, break up the code into functional components so it is clean, readable, and easily tested with succinct unit test functions.
4. Keep in mind some of these algorithms were developed by people with degrees in mathematics and computer sciences. The expectation is for me to learn how they work so I can apply those lessons to solutions I design, and code I develop and maintain.

## Resources

Wikipedia [Quicksort](https://en.wikipedia.org/wiki/Quicksort)

Essential Algorithms: A Practical Approach to Computer Algorithms _[Essential Algorithms, Stephen, Rod. Published 2013, Wiley and Sons]_

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
