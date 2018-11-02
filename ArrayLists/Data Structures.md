### Data Structures

Notes from [opendatastructures.org](opendatastructures.org)

Why need data structures? - A need for efficiency

#### Interfaces vs implementation of the data structure.

* **Interfaces** (abstract data types): Specifies what operations does the data structures provides or supports. For example, a Queue interface would need a method to add (enqueue) or remove (dequeue) elements from the structure. 
* **Implementation**: Specifies the internal implementation details of the funtions of the data structures. There can be many implementations for a given data structure. 

##### Queue, Stack, Deque interfaces

* Interface: add (x), remove(x)
* Operations: add_first(x), remove_first(x), add_last(x), remove_last(x)
* *Queuing disciplines*: FIFO (first in first out), Priority Queue(removes the smallest element), LIFO (Last in First Out) - Stack. 

* **Deque** - Generalization of FIFO and LIFO queues. 

##### List Interface

* Operations: size(), get(i), set(i,x), add(i,x), remove(i)
* Deque interfaces are subsumed by the List Interface. 

##### The Uset Interface: Unordered Sets

* Represents *n* distinct elements in no specific order. 
* Operations: size(), add(x), remove(x), find(x)
* find vs remove - x and y may be distinct but nevertheless treated as equal. Such distinction is useful for creation of dictionaries.

##### The SSet Interface: Sorted Sets

* Store elements in some order such that any two elements x and y can be compared. 
* Operations: size(), add(x), remove(x), find(x)
* Find operation differs from that of Uset. Here smallest elemest *y* such that y>=x is returned. This operation is referred as *successor search*.



#### Mathematics

* **Logarithms**: Another way to think about logarithms: - logb k, - number of times we have to divide k by b before the result is less than or equal to 1. 
* **Factorials**: n! = 1 * 2 * 3* ..... n
* **Binomial co-efficients**: for non-negative integer n, and integer k{0..n} (n k) - n choose k, - number of subsets of an n element set that have size k
* **Asymptotic notation** - **The big-Oh** 
* **Randomization and Probability** - Some algorithms produce different run times due to inherent randomness in the execution. When analysing these data structures, consider the expected or running time. 
  * Expected value of a random number
  * Linearity of expectation. 



#### Model of Computation

* w-bit word RAM model: RAM consists of number of cells with wbit word in each cell. 
* Each basic operation on a cell would take a constant time. Any read or write takes place in constant time. And *w* is lower-bound by w >= logn where n in the number of elements in the data structure. 

**Correctness**: Correctness of the data structure implementation

**Time complexity**: Running times should be as small as possible

**Space complexity**: Use as little memory as possible. 



#### Kinds of running times

1. Worst-case running time
2. Amortized running time: Typical or average time of the operation is f(n)
3. Expected running time: Actual running time is random variable and the expected value of this random variable is f(n)





### ARRAY-BASED LISTS

What is an Array?

Arrays are "lists" of **related** values
https://www.cs.utah.edu/~germain/PPS/Topics/arrays.html

* Implementations of List and Queue interfaces.
  * ArrayStack
  * ArrayDeque
  * DualArrayDeque
  * RootishArrayStack
* Properties of Arrays:
  * get and set run in constant time, whereas adding or inserting an element needs shifting of elements. (they are not dynamic).
  * Cannot expand or shrink, if exceeds from the size of backing array, a new array has to be created. 

#### ArrayStack

* Implements the List interface using an array a called the backing array.
* With *n* as the number of elements stored in the array, property that length(a) > n is maintained using resize() operations. 
* FastArrayStack: copying or cloning of array (say for example. resize) is performed using system level efficient functions instead of for loops. 
* O(1) for get or set, O(n-i) for add or remove an element, O(m) between resize calls, m being the number of adds or remove operations. 

#### ArrayQueue

* Implements FIFO queue.
* Why not use ArrayStack, - Bad idea because operation dealing wit head would require shifiting of entire array. 
* This can be possible using an infinite array, (use modular arthmetic to simulate the infinite array). Offers complexities similar to arraystack.

#### ArrayDeque

* Works on a similar circular technique from arrayQueue, but deque allows for efficient addition and removal at both ends. 
* During addition, we want to limit the time complexity, hence depending on the position of addition, the elements of the array are either left shifted or right shifted. 

#### DualArrayDeque

* Similar performance as ArrayDeque but using two ArrayStacks. A good example of a new data structure by combining two simpler data structure. 
* Places two ArrayStacks, called *front* and *back* back-to-back.

#### RootishArrayStack

- Space efficient compared to previous data structures.
- Arrays frequently are not full. This addresses the problem of wasted space, It stores *n* elements using root(n) arrays. In these arrays, atmost O(root(n)) array locations are unused. Therefore, each array wastes only O(root(n)) space. 
- The array stores its elements in a list of r arrays called blocks. A block b contains b+1 elements. 
- The total space used by a RootishArrayStack is n + O(root(n)).