# Stack/Queue/List

Yuxiang Lin  
CS 201  
2023-02-14

## Implementation of Stack and Queue

[There are two ways to implement a stack or a queue](https://stackoverflow.com/questions/7477181/array-based-vs-list-based-stacks-and-queues):
1. A singly-linked list.
2. A dynamic array. For a queue, it would be a circular buffer based on the dynamic array, which keeps track of the head and tail elements in the array. Both the head and tail pointers wrap around when reached the end of the array.

While a singly-linked list guarantees $O(1)$ time for every single operation, the time cost to allocate and access elements in a non-continuous fashion may be high. A dynamic array gives amortized $O(1)$ time for every single operation. While some operations might take a long time (when it incurred an array resize), the average constant time for each operation is usually lower.

There are also some hybrid approaches: An [unrolled linked list](https://en.wikipedia.org/wiki/Unrolled_linked_list), or a dynamic array pointing to array chunks of constant size that store the actual elements (which is [the implementation of double-ended queue in C++](https://stackoverflow.com/questions/6292332/what-really-is-a-deque-in-stl)).

Note that when your dynamic array is storing the actual objects, they have to be copied when allocating a new array during resizing. The time cost of copying the objects and how the locations of the objects are changed (which might invalidate references) can both be problematic. [Both of these seems to be the reason why C++ implemented std::deque using an array of pointers to arrays instead of a simple circular buffer](https://stackoverflow.com/questions/39324192/why-is-an-stl-deque-not-implemented-as-just-a-circular-vector). However, this problem usually won't occur in Java, where all objects are stored in arrays by reference (excluding primitive type, but they are also wrapped most of the time).

## Concerning Dynamic Array and Amortized Analysis

As the textbook mentioned, instead of resizing the array used for stack/queue each time an element is added or removed, the following scheme can be used: Double the array size when the array is full, half the array when the array is less than a quarter full. The method for analyzing the time cost for each operation in this case would be the amortized analysis. While the time cost of resizing the array to size $n$ is $n$, such cost becomes constant when averaged with each operation.

Therefore, consider only the add operation. __Let each add operation "lend" constant units of credit in time cost__, so it can be spent when the array resizes. [One way to make sure that we never run out of credits](https://anh.cs.luc.edu/363/notes/06A_Amortizing.html) is to consider each array resizing operation at $n = 1, 2, 4, ..., 2^n$ and ensure that the sum of the credits minus the sum of time cost is never less than zero.

Another way to consider this problem is to assume that we have a non-negative number of credits just after the array expanded from $\frac{n}{2}$ to $n$. When the array expands from $n$ to $2n$, it will consume $2n$ time, which can be satisfied by letting the $n - \frac{n}{2}$ add operations deposit $4$ credits each.

## A Better Way to Remove an Item from Linked List

Reference: https://github.com/mkirchner/linked-list-good-taste

Linus Torvalds mentioned a common problem when removing an item from linked list: The previous item will point to the item proceeding the item removed, except when the first item is removed, where there is no previous item and the head pointer needs to be changed. However, he argues that instead of iterating over the each item in the list, we should use a pointer to pointer to iterate over __each pointer__ in the linked list, including the head pointer and the pointers to the next item.

However, while this might be easy to implement in C, its implementation in Java can be problematic as you must implement a "reference to reference" manually to serve the role of a "pointer to pointer" in C.

## Parse Expression with Respect to Operator Precedence

While the textbook only mentioned parsing fully parenthesized infix expressions, Dijkstra's [Shunting Yard Algorithm](https://en.wikipedia.org/wiki/Shunting_yard_algorithm) can in fact parse infix expressions with regards to operator precedence. Basically, the operator stack is used in a way that a operator will yield to the parsing of operators proceeding it with a higher precedence. An even more elegant improvement to this algorithm is to use recursion instead of explicitly using stacks via [Pratt Parsers](http://journal.stuffwithstuff.com/2011/03/19/pratt-parsers-expression-parsing-made-easy/).
