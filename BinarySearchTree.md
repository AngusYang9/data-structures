# Binary Search Tree 二叉查找树

**Binary Search Tree(二叉查找树)** 是树的一种相当常见的形式，因为它们能够高效地访问、查找、插入和删除值，同时保持它们是有序的。

假设有这样一个数字序列：

```javascript
1  2  3  4  5  6  7
```

可以把它从中心变成一棵树：

 ```javascript
               4
            /     \
         2           6
       /   \       /   \
      1     3     5     7
     -^--^--^--^--^--^--^-
      1  2  3  4  5  6  7
 ```

下面是二叉树的工作原理，每个节点可以有两个子节点：

- Left: 小于父节点的值；
- Right: 大于父节点的值。

> 正是由于二叉树的工作原理，树中的所有的值必须是 **唯一** 的。

这使得遍历查找值变得非常高效。假设我们试图在树中找到数字5：

```javascript
             (4)          <--- 5 > 4, so move right.
           /     \
         2        (6)    <--- 5 < 6, so move left.
       /   \      /   \
      1     3   (5)    7 <--- We've reached 5!
```

可以看到我们只需要检查 3 次就可以得到数字 5。如果我们将这棵树扩展到1000个条目。我们会：

```javascript
500 -> 250 -> 125 -> 62 -> 31 -> 15 -> 7 -> 3 -> 4 -> 5
```

1000个项只检查 10 次 !😆

二叉查找树的另一个重要特点是，它们类似于链表，在添加或删除值时，只需要更新周围的项。

```javascript
// usage
var binarySearchTree = new BinarySearchTree();

// root
binarySearchTree.add(4);

// left side
binarySearchTree.add(2);
binarySearchTree.add(1);
binarySearchTree.add(3);

// right side
binarySearchTree.add(6);
binarySearchTree.add(5);
binarySearchTree.add(7);

assert.ok(binarySearchTree.contains(2));
assert.ok(binarySearchTree.contains(3));
assert.ok(binarySearchTree.contains(4));

// duplicate
binarySearchTree.add(6);
```



```javascript
class BinarySearchTree {

  /**
   * Same as the previous Tree, we need to have a "root" of the binary search
   * tree.
   */

  constructor() {
    this.root = null;
  }

  /**
   * In order to test if the value exists in the tree, we first need to search
   * through the tree.
   */

  contains(value) {
    // We start at the root.
    let current = this.root;

    // We're going to keep running as long as we have another node to visit.
    // If we reach a `left` or `right` that is `null` then this loop ends.
    while (current) {

      // If the value is greater than the current.value we move to the right
      if (value > current.value) {
        current = current.right;

        // If the value is less than the current.value we move to the left.
      } else if (value < current.value) {
        current = current.left;

        // Otherwise we must be equal values and we return true.
      } else {
        return true;
      }
    }

    // If we haven't matched anything then we return false.
    return false;
  }

  /**
   * In order to add items to this tree we are going to do the same traversal
   * as before, bouncing between left and right nodes depending on them being
   * less than or greater than the value we're adding.
   *
   * However, this time when we reach a `left` or `right` that is `null` we're
   * going to add a new node in that position.
   */

  add(value) {
    // First let's setup our node.
    let node = {
      value: value,
      left: null,
      right: null
    };

    // Special case for when there isn't any root node and we just need to add
    // one.
    if (this.root === null) {
      this.root = node;
      return;
    }

    // We start at the root.
    let current = this.root;

    // We're going to loop until we've either added our item or discovered it
    // already exists in the tree.
    while (true) {

      // If the value is greater than the current.value we move to the right.
      if (value > current.value) {

        // If `right` does not exist, set it to our node, and stop traversing.
        if (!current.right) {
          current.right = node;
          break;
        }

        // Otherwise just move on to the right node.
        current = current.right;

        // If the value is less than the current.value we move to the left.
      } else if (value < current.value) {

        // If `left` does not exist, set it to our node, and stop traversing.
        if (!current.left) {
          current.left = node;
          break;
        }

        // Otherwise just move on to the left node.
        current = current.left;

        // If the number isn't less than or greater, then it must be the same and
        // we don't do anything.
      } else {
        break;
      }
    }
  }
}
```

