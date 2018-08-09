官方地址：https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/locks/ReadWriteLock.html

```
ReadWriteLock
	 进行写操作时
	 	其他线程无法读取或写入数据
	 进行读操作时
	 	其他线程无法写入数据，但是可以读取数据。
适用于 读多写少的并发场景。
```

