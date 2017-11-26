## Logstash示例2

准备配置文件: logstash-simple.conf

```
input { stdin { } }
output {
  elasticsearch {
  		hosts => ["localhost:9200"]
  		user => elastic
   		password => "C+4Rf7&#_$@hub%8ad#r"

  	}
  stdout { codec => rubydebug }
}
```

> 命令行执行：logstash -f logstash-simple.conf

> 注意：如果安装了X-Pack, 需要在logstash-6.0.0/config/logstash.yml里面配置账号密码才有权限访问

> xpack.monitoring.elasticsearch.username: logstash_system

> xpack.monitoring.elasticsearch.password: logstashpassword

