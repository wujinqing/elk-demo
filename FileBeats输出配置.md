## FileBeats输出配置

### 输出

* Elasticsearch
* Logstash
* Kafka
* Redis
* File
* Console

### Elasticsearch
```
output.elasticsearch:
  hosts: ["https://localhost:9200"]
  username: "admin"
  password: "s3cr3t"
```

### Logstash
```
output.logstash:
  hosts: ["127.0.0.1:5044"]
```

### File

```
output.file:
  path: "/tmp/filebeat"
  filename: filebeat
  #rotate_every_kb: 10000
  #number_of_files: 7
```











































### 参考文献
[configuring-output](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-output.html)







