## FileBeats配置

### filebeat.yml

### name

> 配置beat.name：The name of the Beat. If this option is empty, the hostname of the server is used. The name is included as the beat.name field in each published transaction. You can use the name to group all transactions sent by a single Beat.

```
name: "my-shipper"
```
### tags

> A list of tags that the Beat includes in the tags field of each published transaction. Tags make it easy to group servers by different logical properties. For example, if you have a cluster of web servers, you can add the "webservers" tag to the Beat on each server, and then use filters and queries in the Kibana web interface to get visualisations for the whole group of servers.

```
tags: ["my-service", "hardware", "test"]
```


```
filebeat.prospectors:
- type: log
  paths:
    - /var/log/apache/httpd-*.log

- type: log
  paths:
    - /var/log/messages
    - /var/log/*.log
```

### 配置项

#### type
> log: Reads every line of the log file (default).

> stdin: Reads the standard in.

> redis: Reads slow log entries from redis (experimental).

> udp: Reads events over UDP. Also see max_message_size

#### paths

> /var/log/\*/*.log 当前目录及子目录下所有以.log结尾的文件

> /var/log/*.log 当前目录下所有以.log结尾的文件

#### encoding
> 设置文件的编码方式:plain, latin1, utf-8, utf-16be-bom, utf-16be, utf-16le, big5, gb18030, gbk, hz-gb-2312,euc-kr, euc-jp, iso-2022-jp, shift-jis, and so on

#### exclude_lines
> Filebeat 需要排除的行

```
filebeat.prospectors:
- paths:
    - /var/log/myapp/*.log
  exclude_lines: ['^DBG']
```

#### include_lines
> Filebeat 需要包含的行

```
filebeat.prospectors:
- paths:
    - /var/log/myapp/*.log
  include_lines: ['^ERR', '^WARN']
```

> 如果既有include_lines也有exclude_lines，优先取include_lines，不管include_lines与exclude_lines出现的顺序怎么样。

#### exclude_files
> filebeat会忽略的文件

```
exclude_files: ['\.gz$']
```

#### tags

> A list of tags that the Beat includes in the tags field of each published event. Tags make it easy to select specific events in Kibana or apply conditional filtering in Logstash. These tags will be appended to the list of tags specified in the general configuration.

```
filebeat.prospectors:
- paths: ["/var/log/app/*.json"]
  tags: ["json"]
```




### multiple prospectors

```
filebeat.prospectors:
- type: log
  paths:
    - /var/log/system.log
    - /var/log/wifi.log
- type: log
  paths:
    - "/var/log/apache2/*"
  fields:
    apache: true
  fields_under_root: true
```



### Manage multiline messages 管理多行消息









### 参考文献
[configuration-filebeat-options](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-options.html)


























