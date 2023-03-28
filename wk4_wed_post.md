# Binary Search

Yuxiang Lin  
CS 201  
2023-02-08

## Different ways to partition the interval

[This is the implementation of recursive binary search from the textbook](https://introcs.cs.princeton.edu/java/42sort/BinarySearch.java.html).

```java
public static int search(String key, String[] a, int lo, int hi) {
        if (hi <= lo) return -1;
        int mid = lo + (hi - lo) / 2;
        int cmp = a[mid].compareTo(key);
        if      (cmp > 0) return search(key, a, lo, mid);
        else if (cmp < 0) return search(key, a, mid+1, hi);
        else              return mid;
    }
```

This implementation divides the interval searched into three parts: `[lo, mid), mid, [mid + 1, hi)`

However, there are implementations that divide the interval into two parts:
1. `[lo, mid), [mid, hi)`: These can be used to find the __largest value smaller than the key__ or the __largest value smaller or equal to the key__.
2. `[lo, mid + 1), [mid + 1, hi)`: These can be used to find the __smallest value larger than the key__  or the __smallest value greater or equal to the key__.

__Note for case 2:__

```java
int mid = lo + (hi - lo) / 2;
```
needs to be changed to:

```java
int mid = lo + (hi - lo - 1) / 2;
```
So `mid` would lean towards the smaller element when there are only two elements.

To clarify this kind of division, consider the __largest value smaller than the key__:
1. If `a[mid]` is smaller than the key, it would be a potential answer, but there might be a larger answer.
2. If `a[mid]` is not smaller than the key, than the answer must be smaller than `a[mid]`.

However, partitioning into three parts would also be able to solve these problems, and it would be much more explicit about where should `mid` go.

## Overflow when calculating mid

If the line for calculating `mid` is written like this:

```java
int mid = (lo + hi) / 2;
```

It would be possible to cause integer overflow for a very large array.
