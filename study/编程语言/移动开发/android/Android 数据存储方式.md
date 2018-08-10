在 Android 开发中，主要的数据存储有以下 5 种方式。

```
SharedPreferences
	以键值对的形式存储在 xml 文件中,轻量级存储（如应用的配置、参数属性等）
	默认存储路径：/data/data/包名/shared_prefs
ContentProvider
	Android 四大组件之一，仅作为传输数据的媒介（数据源可多样）
	通过 URL 对象，以达到进程间数据共享、交换等目的
文件存储
	通过 java I/O 流的 读写方法写入文件中,一般存储量大的数据，文件缓存等。
	默认存储路径：/data/data/包名/files 
SQLite 数据库
	嵌入式数据库，使用 SQL 语言，存储结构性数据
	默认存储路径：/data/data/包名/databases
网络存储
	通过网络 获取 远程服务器中的数据
	数据存储在远程服务器中，适用于量大的数据（本地无法存储）、与远程应用共享、交互、更新数据等。
	
```

