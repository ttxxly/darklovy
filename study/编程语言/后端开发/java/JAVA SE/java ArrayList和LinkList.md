#### 相关面试题

##### 1. ArrayList和LinkList的描述，下面说法错误的是？（ ）

```
A. LinkedeList和ArrayList都实现了List接口
B. ArrayList是可改变大小的数组，而LinkedList是双向链接串列
C. LinkedList不支持高效的随机元素访问
D. 在LinkedList的中间插入或删除一个元素意味着这个列表中剩余的元素都会被移动；
	而在ArrayList的中间插入或删除一个元素的开销是固定的
```



```
解析：答案：D
	Arraylist的内存结构是数组，当超出数组大小时创建一个新的数组，把原数组中元素拷贝过去。
		其本质是顺序存储的线性表，插入和删除操作会引发后续元素移动，效率低，但是随机访问效率高
	LinkedList的内存结构是用双向链表存储的，链式存储结构插入和删除效率高，不需要移动。
		但是随机访问效率低，需要从头开始向后依次访问
```

发表于

* https://blog.csdn.net/jdliyao/article/details/79837055