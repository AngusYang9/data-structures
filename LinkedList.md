# Linked List 链表

```javascript
/*** ===================================================================== ***\
 ** - LINKED LISTS -------------------------------------------------------- **
 * ========================================================================= *
 *      _______________________                                              *
 *  ()=(_______________________)=()              ,-----------------,_        *
 *      |                     |               ,"                      ",     *
 *      |   ~ ~~~~~~~~~~~~~   |             ,'    ,---------------,     `,   *
 *      |               ,----------------------------,          ,----------- *
 *      |   ~ ~~~~~~~~ |                              |        |             *
 *      |               `----------------------------'          `----------- *
 *      |   ~ ~~~~~~~~~~~~~   |            `,    `----------------'     ,'   *
 *      |                     |              `,                      ,'      *
 *      |_____________________|                 `------------------'         *
 *  ()=(_______________________)=()                                          *
 **                                                                         **
\*** ===================================================================== ***/
```

**链表(Linked List)** 是数据元素的线性集合，元素的线性顺序不是由它们在内存中的物理位置给出的。 相反，每个元素指向下一个元素。它是由一组节点组成的数据结构，这些节点一起,表示序列。

链表这种结构可以非常有效的进行插入和删除元素O(1)，而遍历与查找则为O(n)。与内存空间连续的数组复杂度相比刚好相反。

<img src="https://img.imyangyong.com/blog/2019-12-19%2015-40-33.jpg" alt="4f63e92598ec2551069a0eef69db7168.jpg" style="zoom:50%;" />

基本的单链表就像下面这样：

1 -> 2 -> 3 -> 4 -> 5

那它们的 json 结构像这样：

```javascript
{
  value: 1,
  next: {
    value: 2,
    next: {
      value: 3,
      next: {...}
    }
  }
}
```

![img](https://img.imyangyong.com/blog/2021-01-28%2019-26-17.png)

```javascript
// usage
const linkedlist = new LinkedList()
linkedlist.add('value1', 0)
linkedlist.add('value2', 1)
linkedlist.get(0).value // value1
linkedlist.remove(0)
console.log(linkedlist) // { head: { value: value2, next: null }, length: 1 }
```

```javascript
class LinkedList {

  /**
   * Unlike a graph, a linked list has a single node that starts off the entire
   * chain. This is known as the "head" of the linked list.
   *
   * We're also going to track the length.
   */

  constructor() {
    this.head = null;
    this.length = 0;
  }

  /**
   * First we need a way to retrieve a value in a given position.
   *
   * This works differently than normal lists as we can't just jump to the
   * correct position. Instead, we need to move through the individual nodes.
   */

  get(position) {
    // Throw an error if position is greater than the length of the LinkedList
    if (position >= this.length) {
      throw new Error('Position outside of list range');
    }

    // Start with the head of the list.
    let current = this.head;

    // Slide through all of the items using node.next until we reach the
    // specified position.
    for (let index = 0; index < position; index++) {
      current = current.next;
    }

    // Return the node we found.
    return current;
  }

  /**
   * Next we need a way to add nodes to the specified position.
   *
   * We're going for a generic add method that accepts a value and a position.
   */

  add(value, position) {
    // Throw an error if position is greater than the length of the LinkedList
    if (position > this.length) {
      throw new Error("Add 'position' parameter should be " + this.length);
    }
    
    // First create a node to hold our value.
    let node = {
      value,
      next: null
    };

    // We need to have a special case for nodes being inserted at the head.
    // We'll set the "next" field to the current head and then replace it with
    // our new node.
    if (position === 0) {
      node.next = this.head;
      this.head = node;

      // If we're adding a node in any other position we need to splice it in
      // between the current node and the previous node.
    } else {
      // First, find the previous node and the current node.
      let prev = this.get(position - 1);
      let current = prev.next;
      // Then insert the new node in between them by setting its "next" field
      // to the current node and updating the previous node's "next" field to
      // the new one.
      node.next = current;
      prev.next = node;
    }

    // Finally just increment the length.
    this.length++;
  }

  /**
   * The last method we need is a remove method. We're just going to look up a
   * node by its position and splice it out of the chain.
   */

  remove(position) {
    // We should not be able to remove from an empty list
    if (!this.head) {
      throw new Error('Removing from empty list')
    }
    // If we're removing the first node we simply need to set the head to the
    // next node in the chain
    if (position === 0) {
      this.head = this.head.next;

      // For any other position, we need to look up the previous node and set it
      // to the node after the current position.
    } else {
      let prev = this.get(position - 1);
      prev.next = prev.next.next;
    }

    // Then we just decrement the length.
    this.length--;
  }
}
```

