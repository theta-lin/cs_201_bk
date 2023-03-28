# Performance

Yuxiang Lin  
CS 201  
2023-02-02

## Tilde notation

$T(N) \sim af(N)$ means $\frac{T(N)}{af(N)} \to 1$ as $N\to \infty$.

Rationale: Running time usually matters only when $N$ is large, where only the non-leading terms would be negligible.

## Order of growth

$f(N)$ is the order of growth.

Usefulness: It is the property of the algorithm, as it is independent of the constant time for each instruction to execute.

## Log-log plot

$\log(T(N)) = \log \left(aN^b \right) = \log{a} + b \log{a}$

## Doubling method

$\frac{T(2N)}{T(N)} = \frac{a(2N)^b}{aN^b} = 2^b$

## Caveats

### Instruction time

Instructions like trigonometric functions are extremely slow. Memory access speed can depend on the access pattern.

### Nondominant inner loop

For smaller inputs, the lower-order terms might have a larger impact. Even if the order of growth for the running time of the algorithm is small, it may have large overhead in parts like initialization.

### System considerations

The configuration of Java and other processes sharing the same system can impact the performance of our program.

### Too close to call

One program can be faster or slower than the other in different situations.

### Strong dependence on input values

Different data of the same size can result in different running times. For example, a sorting algorithm that terminates early when the data is already sorted.

### Multiple problem parameters

## Memory

Object overhead: 16 bytes.  
Padding: Round up the size to a multiple of 8 bytes.
