# Graph 图

```javascript
/*** ===================================================================== ***\
 ** - GRAPHS -------------------------------------------------------------- **
 * ========================================================================= *
 *                                                                           *
 *     A –→ B ←–––– C → D ↔ E																								 *
 *     ↑    ↕     ↙ ↑     ↘																									 *
 *     F –→ G → H ← I ––––→ J																								 *
 *          ↓     ↘ ↑																												 *
 *          K       L                                                        *
 *   																		                                     *
 **                                                                         **
\*** ===================================================================== ***/
```

如上👆示例，我们有一些用 **线** 连接的节点 (A, B, C, D, ...)。

这些节点看起来像这样：

```javascript
Node {
  value: ...,
  lines: [(Node), (Node), ...]
}
```

那么整个图(graph)就是这样：

```javascript
Graph {
  nodes: [
    Node {...},
    Node {...},
    ...
  ]
}
```

usage：

```javascript
var graph = new Graph();
graph.addNode(1);
graph.addNode(2);
graph.addLine(1, 2);
var two = graph.find(1).lines[0];
```

**这看起来似乎工作量很大，但却做得很少，但它实际上是一个非常强大的模式，尤其是在复杂程序中更锐利清晰。**

**它们通过优化数据之间的连接来实现这一点，而不是对数据本身进行操作。一旦在图中有了一个节点，查找图中的所有相关项就非常简单了。**

**很多东西都可以用这种方式来表示，比如 node_modules 文件夹中的 800 个传递依赖项，互联网本身就是一个图(graph)，由链接连接在一起的网页。**

<img src="https://img.imyangyong.com/blog/2021-01-27%2021-10-40.png" alt="node_modules依赖图" style="zoom:50%;" />

```javascript
class Graph {

  /**
   * We'll hold onto all of our nodes in a regular JavaScript array. Not
   * because there is any particular order to the nodes but because we need a
   * way to store references to everything.
   */

  constructor() {
    this.nodes = [];
  }

  /**
   * We can start to add values to our graph by creating nodes without any
   * lines.
   */

  addNode(value) {
    return this.nodes.push({
      value,
      lines: []
    });
  }

  /**
   * Next we need to be able to lookup nodes in the graph. Most of the time
   * you'd have another data structure on top of a graph in order to make
   * searching faster.
   *
   * But for our case, we're simply going to search through all of the nodes to find
   * the one with the matching value. This is a slower option, but it works for
   * now.
   */

  find(value) {
    return this.nodes.find(node => {
      return node.value === value;
    });
  }

  /**
   * Next we can connect two nodes by making a "line" from one to the other.
   */

  addLine(startValue, endValue) {
    // Find the nodes for each value.
    let startNode = this.find(startValue);
    let endNode = this.find(endValue);

    // Freak out if we didn't find one or the other.
    if (!startNode || !endNode) {
      throw new Error('Both nodes need to exist');
    }

    // And add a reference to the endNode from the startNode.
    startNode.lines.push(endNode);
  }
}
```

