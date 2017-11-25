## ELK 日志分析平台

### E
Elasticsearch 是一个分布式的 RESTful 风格的搜索和数据分析引擎，能够解决不断涌现出的各种用例。
作为 Elastic Stack 的核心，它集中存储您的数据，帮助您发现意料之中以及意料之外的情况。

### L

集中、转换和存储数据
Logstash 是开源的服务器端数据处理管道，能够同时 从多个来源采集数据、转换数据，然后将数据发送到您最喜欢的 “存储库” 中。（我们的存储库当然是 Elasticsearch。）

### K

Kibana 让您能够可视化 Elasticsearch 中的数据并操作 Elastic Stack，

### X-Pack
X-Pack 将诸多强大功能集合到一个单独的程序包中，更将它带上了一个新的层次。

如：Security，Alerting，Monitoring，Reporting，Graph，Machine Learning



### Elasticsearch 安装

官方网站
> https://www.elastic.co

下载地址
> https://www.elastic.co/downloads/elasticsearch

解压
> unzip elasticsearch-6.0.0.zip

进入根目录
> cd elasticsearch-6.0.0

启动elasticsearch
> bin/elasticsearch

测试启动是否成功
> curl http://localhost:9200/


### Kibana 安装





### X-Pack安装

安装X-Pack到Elasticsearch
> bin/elasticsearch-plugin install x-pack









































