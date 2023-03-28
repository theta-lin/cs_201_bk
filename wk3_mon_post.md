# Recursion

Yuxiang Lin  
CS 201  
2023-01-30

## Definitions

__Recursion:__ ~~Recursion~~ When something is specified in terms of itself.

## Proof by induction

Recursive program is usually slower than its iterative counterpart, but it is useful to formulate problems recursively in order to proof their correctness by induction:
1. Solution is correct for the base case.
2. Formulate the solution to input `S` as `F(S)`, than formulate `F(S)` as a function of `F(T)` for a simpler problem of `T` (or a function of solutions to multiple simpler problems).

It is also important to know whether the base case will ever be reached or whether the recursion will ever terminate.

## Loop invariant

The inductive proving approach can actually be applied to loops directly with [loop invariant](https://en.wikipedia.org/wiki/Loop_invariant), which is usually equivalent to the induction on the correctness of the equivalent recursive program.

For example, to prove the correctness of the program to find the maximum value in `a[0...n-1]`:
1. The initial maximum value is `a[0]`.
2. Loop `i` from `1` to `n-1`, when the previous maximum value equals to the maximum value in `a[0...i-1]`, the new maximum value will be the maximum value in `a[0...i]`.
3. Loop terminates when `i=n`, with the maximum value equal to the maximum value in `a[0...n-1]`.
