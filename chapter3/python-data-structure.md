# Python data structure {#469f}

> Python 中 list 和 dict 的一些实现细节笔记

### list {#c7af}

Python 中的 list 使用 array 实现，而不是链表（以空间换时间），因此不建议在一些 deque 的场景下用 list 代替。

> list 上执行 insert\(0, element\) 或 pop\(0\) 的时间复杂度为 O\(n\)，而 deque 上执行 appendleft\(element\) 和 pop\(0\) 都是 O\(1\) 复杂度。

当 newsize&gt;allocated 或 newsize&lt;allocated/2 时（即元素满或小于已分配大小的一半），list object 重新分配大小，list 重新分配大小的计算方式可参考 cpython 源码

```
/* This over-allocates proportional to the list size, making room
* for additional growth.  The over-allocation is mild, but is
* enough to give linear-time amortized behavior over a long
* sequence of appends() in the presence of a poorly-performing
* system realloc().
* The growth pattern is:  0, 4, 8, 16, 25, 35, 46, 58, 72, 88, ...
*/
new_allocated = (newsize >> 3) + (newsize < 9 ? 3 : 6);

/* check for integer overflow */
if (new_allocated > PY_SIZE_MAX - newsize) {
    PyErr_NoMemory();
    return -1;
} else {
    new_allocated += newsize;
}
```

### dict {#3dba}

Python 中的 dict 以 hash table 实现，使用开放地址法处理冲突

> 处理哈希表冲突的方式：
> 开放地址法：即发生冲突时重新寻找下一个 solt 直到找到空位置，为此删除元素时需要将存储槽标记为 dummy，否则将会阻断相同 hash 地址的其他元素查找
> 链表法（Ruby使用此种实现）：即对相同 hash 地址的元素使用链表的方式保存在一个 solt 中

当 used solts 和 dummy solts 总量超过数组大小的 2/3 时重新调整字典的大小，在这里，`dictresize()`函数会带一个`minused=24`的参数，24 是`4 * ma_used`。当已使用的slots量很大时（超过50000），`minused=2 * ma_used`。

新表的大小需要大于 24，这是通过将当前表大小向左移位来实现的，每次左移一位直到它大于 24，结果表大小变为了32（即8 -&gt; 16 -&gt; 32）。

新表大小确定后重新 hash 存入元素，注意在删除元素时，永远不会触发数组大小的调整 即使 used solts 远小于总 solts 数。

#### 参考： {#2789}

* _Size of list in memory_
  [_https://stackoverflow.com/questions/7247298/size-of-list-in-memory_](https://stackoverflow.com/questions/7247298/size-of-list-in-memory)
* _Python 列表对象实现原理_
  [_https://foofish.net/python-list-implements.html_](https://foofish.net/python-list-implements.html)
* _Python字典实现_
  [_https://harveyqing.gitbooks.io/python-read-and-write/content/python\_advance/python\_dict\_implementation.html_](https://harveyqing.gitbooks.io/python-read-and-write/content/python_advance/python_dict_implementation.html)

  


