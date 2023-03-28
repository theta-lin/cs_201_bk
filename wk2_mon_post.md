# Arrays

Yuxiang Lin  
CS 201  
2023-01-16

## Definitions

__Data Structure:__ An arrangement of data that enables efficient processing by a program.  
__Array:__ An _indexed_ sequence of values of the same type.

## Abstraction

While the loops mentioned in the last lecture can be an abstraction of possibly infinite length of instructions executed, arrays can be considered an abstraction for "infinite" memory. (The infinite tape of Turing machine?)

## Values of the same type?

1. If you store different types of elements, you would also need another array containing information about the type of each element.
2. To calculate the address of each element easily, each element needs to have the same size.
3. For reference data types, as each slot in the array only stores a reference (address) and that Java has polymorphism for objects, we can create an array of Object, store elements of different types, and then downcast each element to the specific type of that element. Therefore, we can do things similar to how Python store different types in the same list in a sense.

## Why indices start at 0?

One way to consider is that the indices times the size of each element are the offsets from the address of the beginning of the array.

Another way to think about this is given by [E. W. Dijkstra's answer](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD08xx/EWD831.html). He first argues that the difference between the bounds that describe a range of indices should be equal to the length of the range (`a ≤ i < b` or `a < i ≤ b`). Dijkstra then considers there to be a "smallest natural number" (0 or 1 or anything, it doesn't matter). He claims that the lower bound should be included, as when `i` begins at the "smallest natural number", if you exclude the lower bound, `a` would then be an "unnatural number". Therefore, `a ≤ i < b` should be preferred. Finally, when describing an array of length `n` using such a form, starting from 0 will yield a better bound of `0 ≤ i < n` compared to `1 ≤ i < n + 1` when starting from 1.

It is indeed the way ranges are represented in Python.

Nevertheless, there seems to be a trade off when you loop over the array in reverse when you have to start at `n - 1`.
