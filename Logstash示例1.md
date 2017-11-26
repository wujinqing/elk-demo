## Logstash示例1


> logstash -e 'input { stdin { } } output { stdout {} }'

> 注意：如果安装了X-Pack, 需要在logstash-6.0.0/config/logstash.yml里面配置账号密码才有权限访问

> xpack.monitoring.elasticsearch.username: logstash_system

> xpack.monitoring.elasticsearch.password: logstashpassword

