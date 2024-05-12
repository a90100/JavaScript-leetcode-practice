# Note on Corner Cases in Data Structures
## Array

### Corner cases
* Empty sequence
* Sequence with 1 or 2 elements
* Sequence with repeated elements
* Duplicated values in the sequence

## String

### Corner cases
* Empty string
* String with 1 or 2 characters
* String with repeated characters
* Strings with only distinct characters

## Matrix

### Corner cases
* Empty matrix. Check that none of the arrays are 0 length
* 1 x 1 matrix
* Matrix with only one row or column

## Linked List

### Corner cases
* Empty linked list (head is null)
* Single node
* Two nodes
* Linked list has cycles. Tip: Clarify beforehand with the interviewer whether there can be a cycle in the list. Usually the answer is no and you don't have to handle it in the code

## Queue

Most languages don't have a built-in Queue class which can be used, and candidates often use arrays (JavaScript) or lists (Python) as a queue. However, note that the dequeue operation (assuming the front of the queue is on the left) in such a scenario will be O(n) because it requires shifting of all other elements left by one. In such cases, you can flag this to the interviewer and say that you assume that there's a queue data structure to use which has an efficient dequeue operation.

## Interval

### Corner cases
* No intervals
* Single interval
* Two intervals
* Non-overlapping intervals
* An interval totally consumed within another interval
* Duplicate intervals (exactly the same start and end)
* Intervals which start right where another interval ends - [[1, 2], [2, 3]]

## Tree
### Corner cases
* Empty tree
* Single node
* Two nodes
* Very skewed tree (like a linked list)

When using recursion, always remember to check for the base case, usually where the node is null.

You should be very familiar with writing pre-order, in-order, and post-order traversal recursively. As an extension, challenge yourself by writing them iteratively. Sometimes interviewers ask candidates for the iterative approach, especially if the candidate finishes writing the recursive approach too quickly.

## Graph
### Corner cases

* Empty graph
* Graph with one or two nodes
* Disconnected graphs
* Graph with cycles

## Heap

In the context of algorithm interviews, heaps and priority queues can be treated as the same data structure.

## Trie

Be familiar with implementing from scratch, a Trie class and its add, remove and search methods.

### Corner cases

* Searching for a string in an empty trie
* Inserting empty strings into a trie

## Math

### Corner cases

* Division by 0
* Multiplication by 1
* Negative numbers
* Floats
