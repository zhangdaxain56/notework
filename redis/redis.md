#### redis

##### redis是什么？

一种基于缓存的非关系型数据库

NoSQL =Not Only SQL（不仅仅是sql）

这些数据库的存储不需要一个固定的格式。



##### 为什么要用redis，解决了什么问题？

解耦：

1，方便扩展（数据值间没有关系，很好扩展！）

2，大数据量高性能（redis一秒写8万次，读取11万，NoSQL的缓存记录，是一种细颗粒的缓存，性能高）

3，数据类型是多样型的！

4，传统RDBMS 和 NoSQL

```
传统的RDBMS
-结构化组织
-sql
-数据和关系都存在单独的表中
-操作，数据定义语义
-严格的一致性
-基础的事务
```

```
NoSQL
-不仅仅是数据
-没有固定的查询语言
-键值对存储，列存储，文档存储，图形数据库（社交关系）
-最终一致性
-CAP定理和BASE （异地多活）
-高性能，高可用，高扩展性
```

redis是单线程！

cpu不是redis的瓶颈，Redis的瓶颈是根据机器内存和网络带宽



##### 使用redis所遇到的问题是什么？

##### 在项目中如何使用redis的？

##### 怎么解决缓存击穿，缓存穿透和雪崩？

##### RDB和AOF的区别？

##### redis集群？

##### redis的基本指令

```redis
-select  number: 选择对应索引的数据库
-set key value:设置key的值
-get key:获取key的value值
-flushdb: 清空当前数据库
-keys *: 获取全部key值
-exists key: 判断key的值是否为空 空0不空1
-move key: 删除当前key的值
-type key: 获取值的类型
-expire key time:设置过期时间
-ttl key:查询当前key的过期时间
-append key value:向某个key追加值，如果key不存在就相当于set -key value
-incr key:自增1
-decr key:自减1
-incrby key value: 可以自定义增量
-getrange key start end:截取字符串[1,3]
-getrange key 0 -1:获取全部字符串，相当于get key
-setrange key index value：替换指定位置开始的字符串！
-setnx key time value:设置key的value在什么time后过期
-setnx key value: 如果key不存在，创建key，如果key存在创建失败
-mset key1 v1 key2 v2 key3 v3: 批量插入
-mget k1 k2 k3: 批量获取
-msetnx key1 v1 key4 v4:批量插入，如果其中key存在，则都失败，为原子性操作
-set user:1 {name:zhangsan,age:3} :设置一个user:1对象 值为json字符来保存一个对象！
-mset user:1:name zhangsan user:1:age 2: 这里的key是一个巧妙的设计# user:{id}:{filed},如此设计在redis中完全ok了！

-mget user:1:name user:1:age :批量获取user对象的值
-getset name value: 先get 再set，如果不存在值，则返回null
-getset name value1:如果存在值，获取原来的值，并设置新的值
```

数据结构是相同的！

string类型的使用场景：value除了是我们的字符串还可以是数字！

- 计数器
- 统计多单位的数量
- 粉丝数
- 对象缓存存储