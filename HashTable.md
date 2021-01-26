# Hash Table 哈希表(散列)

```javascript
/*** ===================================================================== ***\
 ** - HASH TABLES --------------------------------------------------------- **
 * ========================================================================= *
 *                           ((\                                             *
 *     (              _  ,-_  \ \                                            *
 *     )             / \/  \ \ \ \                                           *
 *     (            /)| \/\ \ \| |          .'---------------------'.        *
 *     `~()_______)___)\ \ \ \ \ |        .'                         '.      *
 *                 |)\ )  `' | | |      .'-----------------------------'.    *
 *                /  /,          |      '...............................'    *
 *        ejm     |  |          /         \   _____________________   /      *
 *                \            /           | |_)                 (_| |       *
 *                 \          /            | |                     | |       *
 *                  )        /             | |                     | |       *
 **                /       /              (___)                   (___)     **
\*** ===================================================================== ***/
```

在计算中, 一个 **哈希表(hash table 或hash map)** 是一个 **无序** 的数据结构。现在完全可以直接使用 es6 Map 替代。

我们使用了 “key” 和 “value”，通过 key 的**哈希值**来获取它独一无二的地址， 其中哈希值是通过 哈希函数/散列函数 计算出来的。

我们利用哈希表的 keys ，可以非常高效的用来增删改查。

> 理想情况下，散列函数将为每个 key 分配给一个唯一的地址，但是大多数哈希表设计采用不完美的散列函数，这可能会导致"哈希冲突(hash collisions)"，也就是散列函数为多个键(key)生成了相同的索引，这种碰撞必须以某种方式进行处理。
>
> 但这里我们不做处理~

![img](http://img.imyangyong.com/blog/2021-01-25%2020-41-31.png)

通过单独的链接解决哈希冲突:

![img](https://img.imyangyong.com/blog/2021-01-25%2020-42-16.png)

```javascript
// usage
const hashMap = new HashTable();
hashMap.set('myKey', 'myValue');
hashMap.get('myKey'); // >> 'myValue'
hashMap.remove('myKey')
```

```javascript
class HashTable {

  /**
   * Again we're going to use a plain JavaScript array to represent our memory.
   */

  constructor() {
    this.memory = [];
  }

  /**
   * In order to store key-value pairs in memory from our hash table we need a
   * way to take the key and turn it into an address. We do this through an
   * operation known as "hashing".
   *
   * Basically it takes a key and serializes it into a unique number for that
   * key.
   *
   *    hashKey("abc") =>  96354
   *    hashKey("xyz") => 119193
   *
   * You have to be careful though, if you had a really big key you don't want
   * to match it to a memory address that does not exist.
   *
   * So the hashing algorithm needs to limit the size, which means that there
   * are a limited number of addresses for an unlimited number of values.
   *
   * The result is that you can end up with collisions. Places where two keys
   * get turned into the same address.
   *
   * Any real-world hash table implementation would have to deal with this,
   * however, we are just going to glaze over it and pretend that doesn't happen.
   */

  /**
   * Let's set up our "hashKey" function.
   *
   * Don't worry about understanding the logic of this function, just know that
   * it accepts a string and outputs a (mostly) unique address that we will use
   * in all of our other functions.
   */

  hashKey(key) {
    let hash = 0;
    for (let index = 0; index < key.length; index++) {
      // Oh look– magic.
      let code = key.charCodeAt(index);
      hash = ((hash << 5) - hash) + code | 0;
    }
    return hash;
  }

  /**
   * Next, let's define our "get" function so we have a way of accessing values
   * by their key.
   *
   * HashTable access is constant O(1) - "AWESOME!!"
   */

  get(key) {
    // We start by turning our key into an address.
    let address = this.hashKey(key);
    // Then we simply return whatever is at that address.
    return this.memory[address];
  }

  /**
   * We also need a way of adding data before we access it, so we will create
   * a "set" function that inserts values.
   *
   * HashTable setting is constant O(1) - "AWESOME!!"
   */

  set(key, value) {
    // Again we start by turning the key into an address.
    let address = this.hashKey(key);
    // Then just set the value at that address.
    this.memory[address] = value;
  }

  /**
   * Finally we just need a way to remove items from our hash table.
   *
   * HashTable deletion is constant O(1) - "AWESOME!!"
   */

  remove(key) {
    // As always, we hash the key to get an address.
    let address = this.hashKey(key);
    // Then, if it exists, we `delete` it.
    if (this.memory[address]) {
      delete this.memory[address];
    }
  }
}
```



