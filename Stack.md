# Stack 栈

```javascript
/*** ===================================================================== ***\
 ** - STACKS -------------------------------------------------------------- **
 * ========================================================================= *
 *                             _ . - - -- .. _                               *
 *         ||||            .-'      /```\     `'-_             /|            *
 *         ||||           (     /`` \___/ ```\    )           | |            *
 *         \__/           |`"-//..__     __..\\-"`|           | |            *
 *          ||            |`"||...__`````__...||"`|           | |            *
 *          ||            |`"||...__`````__...||"`|           \ |            *
 *          ||       _,.--|`"||...__`````__...||"`|--.,_       ||            *
 *          ||    .'`     |`"||...__`````__...||"`|     `'.    ||            *
 *          ||   '.        `/ |...__`````__...| \         .'   ||            *
 *          ||     `'-..__  ``      `````      ``  __..-'`     ||            *
 *                        `""---,,,_______,,,---""`                          *
 **                                                                         **
\*** ===================================================================== ***/
```

在计算机科学中, 一个 **stack（栈）** 是一种抽象数据类型，表示元素的集合，具有两种主要操作：

- **push，**添加元素到栈的顶端(末尾)；
- **pop，**移除栈最顶端(末尾)的元素。

以上两种操作可以简单概括为”后进先出（LIFO = last in, first out）“。

此外,应有一个 `peek` 操作用于访问栈当前顶端(末尾)的元素。

”栈“ 这个名称,可类比于一组物体的堆叠（一摞书,一摞盘子之类的）。

栈的 push 和 pop 操作的示意：

![img](https://img.imyangyong.com/blog/2021-01-26%2017-18-17.png)

```javascript
// usage
const stack = new Stack()
stack.push('abc') // ['abc']
stack.peek() // 'abc'
stack.pop() // []
```

```javascript
class Stack {

  /**
   * We're going to again be backed by a JavaScript array, but this time it
   * represents a list like we implemented before rather than memory.
   */

  constructor() {
    this.list = [];
    this.length = 0;
  }

  /**
   * We're going to implement two of the functions from list's "push" and "pop"
   * which are going to be identical in terms of functionality.
   */

  /**
   * Push to add items to the top of the stack.
   */

  push(value) {
    this.length++;
    this.list.push(value);
  }

  /**
   * And pop to remove items from the top of the stack.
   */

  pop() {
    // Don't do anything if we don't have any items.
    if (this.length === 0) return;

    // Pop the last item off the end of the list and return the value.
    this.length--;
    return this.list.pop();
  }

  /**
   * We're also going to add a function in order to view the item at the top of
   * the stack without removing it from the stack.
   */

  peek() {
    // Return the last item in "items" without removing it.
    return this.list[this.length - 1];
  }
}
```

