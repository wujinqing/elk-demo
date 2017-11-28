## filebeat.yml配置

[参考文档](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-configuration.html)


```
filebeat.prospectors:
- type: log
  enabled: true
  paths:
    - /var/log/*.log
    #- c:\programdata\elasticsearch\logs\*
```

/var/log/*.log
> /var/log/目录下所有以.log结尾的文件

/var/log/\*/*.log
> /var/log/目录及子目录下所有以.log结尾的文件

### 输出

直接输出到elasticsearch

```
output.elasticsearch:
  hosts: ["192.168.1.42:9200"]
```



输出到logstash

```
output.logstash:
  hosts: ["127.0.0.1:5044"]
```

配置为Filebeat提供的简单的Kibana dashboards
```
setup.kibana:
  host: "localhost:5601"
```

如果集成了X-Pack的secured需要设置用户名密码

```
output.elasticsearch:
  hosts: ["myEShost:9200"]
  username: elastic
  password: elastic
setup.kibana:
  host: "mykibanahost:5601"
  username: elastic
  password: elastic
```




























