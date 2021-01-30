# Tree 树

```javascript
/*** ===================================================================== ***\
 ** - TREES --------------------------------------------------------------- **
 * ========================================================================= *
 *            ccee88oo             \ | /                                     *
 *          C8O8O8Q8PoOb o8oo    '-.;;;.-,   ooooO8O8QOb o8bDbo              *
 *        dOB69QO8PdUOpugoO9bD  -==;;;;;==-aadOB69QO8PdUOpugoO9bD            *
 *       CgggbU8OU qOp qOdoUOdcb .-';;;'-.  CgggOU ddqOp qOdoUOdcb           *
 *           6OuU  /p u gcoUodpP   / | \ jgs  ooSec cdac pdadfoof            *
 *             \\\//  /douUP         '         \\\d\\\dp/pddoo               *
 *               \\\////                         \\ \\////                   *
 *                |||/\                           \\///                      *
 *                |||\/                           ||||                       *
 *                |||||                          /|||                        *
 ** .............//||||\.......................//|||\\..................... **
\*** ===================================================================== ***/
```

我们将从一个极其简单的树形结构开始。它没有任何特殊的规则，看起来像这样：

```javascript
/**
 *          A            *
 *        ↙   ↘          *
 *      B       C        */
Tree {
  root: {
    value: 'A',
    children: [{
      value: 'B',
      children: [...]
    }, {
      value: 'C',
      children: [...]
    }]
  }
}
```

```javascript
// usage
var tree = new Tree();

tree.add(1);
tree.add(2, 1);
tree.add(3, 1);
tree.add(4, 2);
tree.add(5, 2);

var traversed = [];
tree.traverse(function(node) {
  traversed.push(node.value);
});

assert.deepEqual(traversed, [1, 2, 4, 5, 3]);
```

```javascript
class Tree {

  /**
   * The tree has to start with a single parent, the "root" of the tree.
   */

  constructor() {
    this.root = null;
  }

  /**
   * We need a way to traverse our tree and call a function on each node in the
   * tree.
   */

  traverse(callback) {
    // We'll define a walk function that we can call recursively on every node
    // in the tree.
    function walk(node) {
      // First call the callback on the node.
      callback(node);
      // Then recursively call the walk function on all of its children.
      node.children.forEach(walk);
    }

    // Now kick the traversal process off.
    walk(this.root);
  }

  /**
   * Next we need a way to add nodes to our tree.
   */

  add(value, parentValue) {
    let newNode = {
      value,
      children: []
    };

    // If there is no root, just set it to the new node.
    if (this.root === null) {
      this.root = newNode;
      return;
    }

    // Otherwise traverse the entire tree and find a node with a matching value
    // and add the new node to its children.
    this.traverse(node => {
      if (node.value === parentValue) {
        node.children.push(newNode);
      }
    });
  }
}
```

