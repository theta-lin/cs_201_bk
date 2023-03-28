# Symbol Table

Yuxiang Lin  
CS 201  
2023-02-15

## Tree Rotation

For a node `F` and its child node `C` in a binary search tree, `C` can be rotated to `F`'s place without invalidating the properties of a BST.

Assume that `C` is the right child node of `F`, `x` and `y` is the left and right subtree of `C`, and `z` is the right subtree of `F`. Below is the rotation:

```
    F             C
   / \           / \
  C   z    =>   x   F
 / \               / \
x   y             y   z
```

## Treap

Reference: https://en.wikipedia.org/wiki/Treap

A simple way to balance a BST is assign a __random priority__ to each node in the BST and maintain a heap order such that the priority of each node is not smaller than its children.

For insertion, after inserting the node, recursively perform tree rotation on the inserted node and its parent node to maintain the heap order.

For deletion, only the case that the node deleted has two children is non-trivial. In such a case, recursively rotate the higher-priority child of the node to be deleted up until the node to be deleted has less than two children.

By maintaining such a heap order property, it would be equivalent to constructing a BST from scratch by inserting the same nodes in the same random order. Therefore, the expected height of such a BST would be the same as the expected height of a random binary tree, which is logarithmic to the number of the nodes in the tree.
