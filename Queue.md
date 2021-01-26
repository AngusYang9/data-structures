# Queue 队列

```javascript
/*** ===================================================================== ***\
 ** - QUEUES -------------------------------------------------------------- **
 * ========================================================================= *
 *                   /:""|                     ,@@@@@@.                      *
 *                  |: oo|_                   ,@@@@@`oo                      *
 *                  C     _)                  @@@@C   _)                     *
 *                    ) /                     "@@@@ '=                       *
 *                   /`\\                      ```)/                         *
 *                  || | |                       /`\\                        *
 *                  || | |                      || | \                       *
 *                  ||_| |                      || | /                       *
 *                  \( ) |                      ||_| |                       *
 *               |~~~`-`~~~|                    |))) |                       *
 *         (_)   |         |         (_)        |~~~/          (_)           *
 *         | |`""....__     __....""`| |`""...._|| /  __....""`| |           *
 *         | |`""....__`````__....""`| |`""....__`````__....""`| |           *
 *         | |       | ||```         | |        ||`|``         | |           *
 *         | |       |_||__          | |        ||_|__         | |           *
 *        ,| |, jgs  (____))        ,| |,       ((;:;:)       ,| |,          *
 **       `---`                     `---`                     `---`         **
\*** ===================================================================== ***/
```

在计算机科学中, 一个 **queue（队列）** 是一种特殊类型的抽象数据类型或集合。集合中的实体按顺序保存。

队列基本操作有两种：入队和出队。从队列的后端位置添加实体，称为入队；从队列的前端位置移除实体，称为出队。

队列中元素先进先出 FIFO (first in, first out) 的示意：

![img](https://img.imyangyong.com/blog/2021-01-26%2017-52-21.png)

```javascript
// usage
const queue = new Queue()
queue.enqueue('a') // ['a']
queue.enqueue('b') // ['a', 'b']
queue.peek() // a
queue.dequeue() // a; ['b']
```

```javascript
class Queue {

  /**
   * Again, our queue is using a JavaScript array as a list rather than memory.
   */

  constructor() {
    this.list = [];
    this.length = 0;
  }

  /**
   * Similar to stacks we're going to define two functions for adding and
   * removing items from the queue. The first is "enqueue".
   *
   * This will push values to the end of the list.
   */

  enqueue(value) {
    this.length++;
    this.list.push(value);
  }

  /**
   * Next is "dequeue", instead of removing the item from the end of the list,
   * we're going to remove it from the start.
   */

  dequeue() {
    // Don't do anything if we don't have any items.
    if (this.length === 0) return;

    // Shift the first item off the start of the list and return the value.
    this.length--;
    return this.list.shift();
  }

  /**
   * Same as stacks we're going to define a "peek" function for getting the next
   * value without removing it from the queue.
   */

  peek() {
    return this.list[0];
  }
}
```



