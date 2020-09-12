#### 1. zookeeper集群见zookeeper集群模式

#### 2 .kafka

官方下载kafka_2.12-2.6.0.tgz：http://kafka.apache.org/downloads

下载不带src的版本

解压kafka_2.12-2.6.0.tgz

```bash
tar -zxvf kafka_2.12-2.6.0.tgz
```

修改config中的server.properties中的配置：

```bash
broker.id=3 #节点数，此可以不用配置，如果配置要和log.dirs的路径中meta.properties中配置的一样
listeners = PLAINTEXT://192.168.101.8:9095 #修改为本机ip，查看端口号是否被占用 netstat -anp|grep 端口号

num.partitions=3
offsets.topic.replication.factor=3
transaction.state.log.replication.factor=3
transaction.state.log.min.isr=3
default.replication.factor=3
#尽量不要设置为1
zookeeper.connect=192.168.101.8:2181,192.168.101.6:2181,192.168.101.7:2181 #zookeeper集群地址

# Timeout in ms for connecting to zookeeper
zookeeper.connection.timeout.ms=18000 #此处可以设置得大一点


```

可能出现得问题 

broker.id=3和log.dirs的路径中meta.properties中配置的不一样，运行可能报错

cluster.id=GVTQXlBjR6ebQAziSKwYhQ和运行时得cluster.id中得一样

