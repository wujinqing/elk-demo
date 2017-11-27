## How Filebeat works


### 两个重要的组件：
* harvesters
* prospectors


两个组件一起完成数据的收集和发送到输出端(elasticsearch/logstash)。

### harvester是什么
> 每一个单独的文件都会对应一个harvester，harvester逐行读取每一个文件，然后发送到输出端(elasticsearch/logstash)。

> 一个harvester开始于每一个文件。harvester负责文件的开启和关闭。

> 如果一个文件被删除或者移动了，Filebeat会继续读取文件， 直到harvester关闭掉了才会释放磁盘空间。

> 默认情况下，Filebeat会一直打开这个文件直到触发了close_inactive。


关闭harvester会有如下影响：
> 文件句柄被关闭，如果在harvester读取过程中文件被删除了，资源将会被释放
     The file handler is closed, freeing up the underlying resources
     if the file was deleted while the harvester was still reading the file.

> 只有当过了scan_frequency设置的时间之后harvesting才能重新开始

> 如果在harvester关闭之后文件被删除，harvesting将无法继续



### prospector是什么

> 一个prospector负责管理harvesters和找出所有将要被读取的资源。

> 如果输入类型是log，prospector会找出所有匹配的文件并为每个文件启动一个harvester，每一个prospector运行在自己的Go routine中

```
filebeat.prospectors:
- type: log
  paths:
    - /var/log/*.log
    - /var/path2/*.log
```

>  Filebeat目前支持两种类型的prospector：log 和 stdin。


> 每个prospector可以被定义多次，log类型的prospector会检查每一个文件，确认是否需要为他启动一个harvester。

> 是否已经启动、是否需要忽略这个文件。

> 新的数据只有当文件大小发生变化才会重新获取，由于harvester已经关闭了

### Filebeat的prospectors只能读取本地文件，无法读取远程的文件

> Filebeat prospectors can only read local files.

> There is no functionality to connect to remote hosts to read stored files or logs.


### Filebeat如何保存文件的状态?
> 通过registry 文件来保存的。

> Filebeat会频繁的将每一个文件的状态刷新到registry文件中(在data目录中)，文件会记录最近一次读取的offset

> 当Elasticsearch 或者 Logstash重启之后将会根据这个offset来恢复读取位置


### Filebeat如何保证至少一次传输， 保证数据不会丢失？
> Filebeat是通过将每一次的delivery state保存到registry文件来实现  保证数据不会丢失的。

> 当output阻塞了或者没有确认任何事件，Filebeat将一直重试直到output返回已经收到数据的事件。

> 当Filebeat关闭，不会等待output的ACK，所有已发送并且还没来得及响应的数据将会在Filebeat重启后被重新发送, 这就保证了at least once。

> 你可以通过shutdown_timeout配置Filebeat在关闭之前的等待时间。

### Filebeat在以下两种情况下可能不保证at least once

> 1.If log files are written to disk and rotated faster than they can be processed by Filebeat.

> 2.if files are deleted while the output is unavailable.


参考文献：
[how filebeat works](https://www.elastic.co/guide/en/beats/filebeat/current/how-filebeat-works.html)
















































