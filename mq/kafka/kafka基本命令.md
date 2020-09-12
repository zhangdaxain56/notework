```bash
启动kafka ： bin/kafka-server-start.sh -daemon config/server.properties

关闭：bin/kafka-server-stop.sh config/server.properties
```

kafka和Zookeeper已启动完成

1. 创建topic

```bash
bin/kafka-topics.sh --create --zookeeper 192.168.101.8:2181 --replication-factor 3 --partitions 3 --topic test
```

2.查看主题

```bash
bin/kafka-topics.sh --list --zookeeper 192.168.101.8:2181
```

3.发送消息

```bash
bin/kafka-console-producer.sh --broker-list 192.168.101.8:2181 --topic test
```

4.接收消息

```bash
bin/kafka-console-consumer.sh --bootstrap-server 192.168.101.8:9095 --topic test --from-beginning
```

5 . 查看特定主题的详细信息 

```bash
bin/kafka-topics.sh --zookeeper localhost:2181 --describe  --topic test
```

6.删除主题

```bash
bin/kafka-topics.sh --zookeeper localhost:2181 --delete  --topic test
```


