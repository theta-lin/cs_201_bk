# In-place Rotation of Array

Yuxiang Lin  
CS 201  
2023-01-31

This topic is not covered by lecture, but when our TA mentioned a way to rotate array in-place during Wednesday recitation, it instantly grabbed my attention. While I have always been mindful of the running time of the programs I wrote, the memory consumption of them often slipped my mind. If I were to rotate an array, I would simply allocate a new temporary array and use a linear loop to copy the values to the temporary array. Nevertheless, there are indeed ways to rotate arrays in-place (maybe with a temporary variable for one element from the array).

Assume we are rotating an array `a` of `n` elements `k` places to the right.

Reference: https://github.com/scandum/rotate

## Juggling Rotation

This is the algorithm introduced by our TA. The basic idea is to move `a[i]` to `a[(i + k) % n]`, then `a[(i + k) % n]` needs to be moved to `a[(i + 2 * k) % n]`, then `a[(i + 2 * k) % n]` to `a[(i + 3 * k) % n]`, and so on. This would continue until `i + q * k == i mod n` for the smallest positive `q`. Therefore, `q = n / gcd(n, k)` and the number of such cycles is `gcd(n, k)`, which means we only need to rotate each cycle starting from `0...gcd(n, k)-1`.

## Triple Reversal Rotation

Let `x` be `a[0...k-1]` and `y` be `a[k...n-1]`. Simply reverse `x` and `y` before reversing the entire array. There is also an optimization that maintains 4 pointers, which does an equivalent of three rotations at once.

```
+-----+-----+
|< x <|< y <|
+-----+-----+

+-----+-----+
|> x >|> y >|
+-----+-----+

+-----+-----+
|< y <|< x <|
+-----+-----+
```

## Gries-Mills Rotation

Assume that the `x` part is longer than the `y` part (always choose the longer of the part to the left and right of `k`), let `x1` be the right part of `x` that is equal in length to `y`. Swap `x1` and `y`. Now that `x1` is already in the correct location, the problem is thus reduced to rotating the `x0` and `y` part, which can be recursively solved by the same algorithm.

```
+-----------+-------+-------+
|<    x0   <|<  x1 <|<  y  <|
+-----------+-------+-------+

+-----------+-------+-------+
|<    x0   <|<  y  <|<  x1 <|
+-----------+-------+-------+
```

## Successive Rotation

This algorithm is also first described by Gries and Mills. It is similar to the algorithm above, `y` is also shorter than `x`, but this time let `x0` be the left part of `x` that is equal in length to `y`. Swap `x0` and `y`, notice that this algorithm puts `y` in the correct location first. Now that the `x1` and `x0` becomes a smaller problem to be solved recursively. There is another kind of algorithm that uses both Gries-Mills rotation and successive rotation to improve memory access pattern.

```
+-------+-----------+-------+
|<  x0 <|<    x1   <|<  y  <|
+-------+-----------+-------+

+-------+-----------+-------+
|<  y  <|<    x1   <|<  x0 <|
+-------+-----------+-------+
```

## Another Thought About In-place Merge Sort

Merge sort came to my mind immediately when mentioning in-place algorithms, as I only know the simple implementation of merge sort that is __NOT__ in-place.

But in fact, [in-place merge sort is a thing](https://stackoverflow.com/questions/2571049/how-to-sort-in-place-using-the-merge-sort-algorithm). Basically, when you sort one half of the array, the other half can be used as a temporary array. But a small trick would be needed to merge the two halves of the whole array.

Another interesting in-place variation of merge sort is [block sort](https://en.wikipedia.org/wiki/Block_sort).
