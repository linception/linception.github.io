---
title: Docker 方式安装 Elasticsearch
---



# Elasticsearch

## 安装

版本兼容：https://www.elastic.co/cn/support/matrix#matrix_compatibility

### Docker

```bash
# 安装 es
docker pull elasticsearch:7.6.2
docker run -d --name es -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2
# 访问 9200

# 允许跨域
docker exec -it es /bin/bash
cd config
vi elasticsearch.yml
# 配置
http.cors.enabled: true
http.cors.allow-origin: "*"
docker restart es

# 安装 kibana 
docker pull kibana:7.6.2
docker run -d --name kibana --link es:elasticsearch -p 5601:5601 kibana:7.6.2
# 访问5601

# kibana 配置中文
docker exec -it kibana /bin/bash
cd config
vi kibana.yml
# 增加
i18n.locale: "zh-CN"
docker restart kibana
```

参考：https://www.cnblogs.com/adawoo/p/12455265.html

### Linux

```bash
useradd es
passwd es
chown es:es -R elasticsearch-7.6.0/
```

*`config/elasticsearch.yml`*

```yml
network.host: 0.0.0.0
cluster.initial_master_nodes: ["node-1", "node-2"]
```

***ERROR: [4] bootstrap checks failed
[1]: max file descriptors [4096] for elasticsearch process is too low, increase to at least [65535]
[2]: max number of threads [3155] for user [es] is too low, increase to at least [4096]
[3]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]***

*`/etc/security/limits.conf`*

```ini
* soft nofile 65536
* hard nofile 65536
* soft nproc 4096
* hard nproc 4096
```

*`/etc/sysctl.conf`*

```ini
vm.max_map_count = 655360

#/sbin/sysctl -p
```

访问 9200

### Windows

## 基本理论

### 倒排索引

## 配置

- 跨域

## 插件

- head

## ELK

### Logstash

### Kibana

- 中文

## IK 分词器

github 地址：https://github.com/medcl/elasticsearch-analysis-ik

### 安装

安装方式一：

```bash
docker exec -it es /bin/bash
cd plugins
elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.6.2/elasticsearch-analysis-ik-7.6.2.zip
docker restart es
```

安装方式二：

```bash
cd plugins && mkdir ik && cd ik
curl -LJO https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.6.2/elasticsearch-analysis-ik-7.6.2.zip
# 加速 curl -LJO https://hub.fastgit.org/medcl/elasticsearch-analysis-ik/releases/download/v7.6.2/elasticsearch-analysis-ik-7.6.2.zip
unzip elasticsearch-analysis-ik-7.6.2.zip
```

### 添加字典

```bash
#docker exec -it -e LANG=C.UTF-8 es /bin/bash
docker exec -it es /bin/bash
# elasticsearch-plugin 方式安装配置文件在
cd config/analysis-ik
# 手动解压配置文件在
cd plugins/ik/config
# 中文乱码不管，也可以添加成功
vi my.dic
vi IKAnalyzer.cfg.xml
# 添加
<entry key="ext_dict">my.dic</entry>
docker restart es
```

### 测试

```json
GET _analyze
{
  "analyzer": "ik_smart",
  "text": "黎小荣"
}
```

分词方式：

- ik_smart
- ik_max_word