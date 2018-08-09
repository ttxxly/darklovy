ArrayList是 List 接口的可变数组实现，底层使用数组保存所有元素。其操作基本上是对数组的操作。

#### ArrayList 概述

ArrayList 相当于动态数组，每个 ArrayList 实例都有一个容量，该容量是指用于存储列表元素的数组的大小，它总是至少等于列表的大小。随着向ArrayList中不断添加元素，其容量自动增长。

**自动增长会带来数据向新数组的重新拷贝** 

#### ArrayList 的常见方法

##### 1. set() 方法

```
// 用指定的元素替代此列表中指定位置上的元素，并返回以前位于该位置上的元素。  
public E set(int index, E element) {  
    RangeCheck(index);  
  
    E oldValue = (E) elementData[index];  
    elementData[index] = element;  
    return oldValue;  
}  
```

##### 2. add() 方法

```
// 将指定的元素添加到此列表的尾部。  
public boolean add(E e) {  
    ensureCapacity(size + 1);   
    elementData[size++] = e;  
    return true;  
}  
```

```
// 将指定的元素插入此列表中的指定位置。  
// 如果当前位置有元素，则向右移动当前位于该位置的元素以及所有后续元素（将其索引加1）。  
public void add(int index, E element) {  
    if (index > size || index < 0)  
        throw new IndexOutOfBoundsException("Index: "+index+", Size: "+size);  
    // 如果数组长度不足，将进行扩容。  
    ensureCapacity(size+1);  // Increments modCount!!  
    // 将 elementData中从Index位置开始、长度为size-index的元素，  
    // 拷贝到从下标为index+1位置开始的新的elementData数组中。  
    // 即将当前位于该位置的元素以及所有后续元素右移一个位置。  
    System.arraycopy(elementData, index, elementData, index + 1, size - index);  
    elementData[index] = element;  
    size++;  
}  
```

```
// 按照指定collection的迭代器所返回的元素顺序，将该collection中的所有元素添加到此列表的尾部。  
public boolean addAll(Collection<? extends E> c) {  
    Object[] a = c.toArray();  
    int numNew = a.length;  
    ensureCapacity(size + numNew);  // Increments modCount  
    System.arraycopy(a, 0, elementData, size, numNew);  
    size += numNew;  
    return numNew != 0;  
}  
```

```
// 从指定的位置开始，将指定collection中的所有元素插入到此列表中。  
public boolean addAll(int index, Collection<? extends E> c) {  
    if (index > size || index < 0)  
        throw new IndexOutOfBoundsException(  
            "Index: " + index + ", Size: " + size);  
  
    Object[] a = c.toArray();  
    int numNew = a.length;  
    ensureCapacity(size + numNew);  // Increments modCount  
  
    int numMoved = size - index;  
    if (numMoved > 0)  
        System.arraycopy(elementData, index, elementData, index + numNew, numMoved);  
  
    System.arraycopy(a, 0, elementData, index, numNew);  
    size += numNew;  
    return numNew != 0;  
}  
```

##### 3. get() 方法

```
// 返回此列表中指定位置上的元素。  
public E get(int index) {  
    RangeCheck(index);  
  
    return (E) elementData[index];  
}  
```

##### 4. remove() 方法

```
// 移除此列表中指定位置上的元素。  
public E remove(int index) {  
    RangeCheck(index);  
  
    modCount++;  
    E oldValue = (E) elementData[index];  
  
    int numMoved = size - index - 1;  
    if (numMoved > 0)  
        System.arraycopy(elementData, index+1, elementData, index, numMoved);  
    elementData[--size] = null; // Let gc do its work  
  
    return oldValue;  
}  
```

```
// 移除此列表中首次出现的指定元素（如果存在）。这是应为ArrayList中允许存放重复的元素。  
public boolean remove(Object o) {  
    // 由于ArrayList中允许存放null，因此下面通过两种情况来分别处理。  
    if (o == null) {  
        for (int index = 0; index < size; index++)  
            if (elementData[index] == null) {  
                // 类似remove(int index)，移除列表中指定位置上的元素。  
                fastRemove(index);  
                return true;  
            }  
} else {  
    for (int index = 0; index < size; index++)  
        if (o.equals(elementData[index])) {  
            fastRemove(index);  
            return true;  
        }  
    }  
    return false;  
}  
```

*注意：从数组中移除元素的操作，也会导致被移除的元素以后的所有元素的向左移动一个位置。*

##### 调整容量

```
public void ensureCapacity(int minCapacity) {  
    modCount++;  
    int oldCapacity = elementData.length;  
    if (minCapacity > oldCapacity) {  
        Object oldData[] = elementData;  
        int newCapacity = (oldCapacity * 3)/2 + 1;  
            if (newCapacity < minCapacity)  
                newCapacity = minCapacity;  
      // minCapacity is usually close to size, so this is a win:  
      elementData = Arrays.copyOf(elementData, newCapacity);  
    }  
}  
```

##### 参考资料

* http://zhangshixi.iteye.com/blog/674856

支持我的话可以关注下我的微信公众号，每天都会推送新知识~

> ![](C:\Users\ttxxl\Pictures\20180404220912740.jpg)![](C:\Users\ttxxl\Pictures\qrcode_for_gh_e125acf2ab2b_258.jpg)

 

##### 发表地址

* https://blog.csdn.net/jdliyao/article/details/81178013
* https://www.jianshu.com/p/f30225efda94
* https://juejin.im/post/5b5687455188251aff2163e0
