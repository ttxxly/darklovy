## Map 类型

先看例子 m1:

```
func main() {
    m := make(map[int]int)
    mdMap(m)
    fmt.Println(m)
}

func mdMap(m map[int]int) {
    m[1] = 100
    m[2] = 200
}
```

结果是

```
map[2:200 1:100]
```

我们再修改如下 m2：

```
func main() {
    var m map[int]int
    mdMap(m)
    fmt.Println(m)
}

func mdMap(m map[int]int) {
    m = make(map[int]int)
    m[1] = 100
    m[2] = 200
}
```

发现结果变成了

```
map[]
```

要理解这个问题，需要明确在 Go 中不存在引用传递，所有的参数传递都是值传递。

现在再来分析下，如图:

![img](https://images2017.cnblogs.com/blog/1046505/201709/1046505-20170905155707241-1391630050.png)

可能有些人会有疑问，为什么途中的 m 像是一个指针呢。查看[官方的 Blog](https://blog.golang.org/go-maps-in-action) 中有写：

> Map types are reference types, like pointers or slices, ...

这边说 Map 类型是引用类型，像是指针或是 Slice（切片）。所以我们基本上可以把它当作是指针来看待（**注意**，只是近似，或者说其中含有指针，其内部仍然含有其他信息，这里只是为了便于理解），只不过这个指针有些特殊罢了。

m1 中，当调用 `mdMap` 方法时重新开辟了内存，将 m 的内容，也就是 map 的地址拷贝入了 m'，所以此时当操作 map 时，m 和 m' 所指向的内存为同一块，就导致 m 的 map 发生了改变。

而在 m2 中，在调用 `mdMap` 之前，m 并未分配内存，也就是说并未指向任何的 map 内存区域。从未导致 m' 的 map 修改不能反馈到 m 上。

## Slice 类型

现在看一下 Slice。

s1:

```
func main() {
    s := make([]int, 2)
    mdSlice(s)
    fmt.Println(s)
}

func mdSlice(s []int) {
    s[0] = 1
    s[1] = 2
}
```

s2:

```
func main() {
    var s []int
    mdSlice(s)
    fmt.Println(s)
}

func mdSlice(s []int) {
    s = make([]int, 2)
    s[0] = 1
    s[1] = 2
}
```

不出所料：

s1 结果为

```
[1 2]
```

s2 为

```
[]
```

因为正如官方所说，Slice 类型与 Map 类型一样，类似于指针，Slice 中仍然含有长度等信息。

修改一下 s1，变成 s3：

```
func main() {
    s := make([]int, 2)
    mdSlice(s)
    fmt.Println(s)
}

func mdSlice(s []int) {
    s = append(s, 1)
    s = append(s, 2)
}
```

不再修改 slice 原先的两个元素，而加上另外两个，结果为:

```
[0 0]
```

发现修改并没有反馈到原先的 slice 上。

这里我们需要把 slice 想象为特殊的指针，其已经保存了所指向内存区域长度，所以 `append` 之后的内存并不会反映到 `main()` 中：

![img](https://images2017.cnblogs.com/blog/1046505/201709/1046505-20170905155742351-627798232.png)

那如何才能反映到 `main()` 中呢？没错，使用指向 Slice 的指针。

```
func mdSlice(s *[]int) {
    *s = append(*s, 1)
    *s = append(*s, 2)
}
```

内存如图所示：

![img](https://images2017.cnblogs.com/blog/1046505/201709/1046505-20170905155756397-1995895123.png)

> 注意本文中内存区域分配是否连续完全随机，不影响程序，只是为了图解清晰。

## Chan 类型

Go 中 `make` 函数能创建的数据类型就 3 类：Slice, Map, Chan。不比多说，相比读者已经能想象 Chan 类型的内存模型了。的确如此，读者可以自己尝试，这边就不过多赘述了。（可以通通过 == nil 的比较来进行测试）。



关于slice或map操作，下面正确的是（）

![img](https://uploadfiles.nowcoder.net/images/20171203/3367369_1512279828612_E135777046538A1F75605878FC012839)

- ```
  A
  ```

- ```
  B
  ```

- ```
  C
  ```

- ```
  D
  ```


正确答案：A C D