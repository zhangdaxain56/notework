# zookeeper集群配置搭建（三节点）

![img](https://csdnimg.cn/release/phoenix/template/new_img/original.png)

[北洋的青春](https://me.csdn.net/xzm5708796) 2019-01-08 19:38:12 ![img](https://csdnimg.cn/release/phoenix/template/new_img/articleReadEyes.png) 207 ![img](https://csdnimg.cn/release/phoenix/template/new_img/tobarCollect.png) 收藏

分类专栏： [运维类](https://blog.csdn.net/xzm5708796/category_8271040.html)

版权

注意:节点数最好是奇数

## 0.环境记录：

| IP        | 机器名    | 端口      |
| --------- | --------- | --------- |
| 172.0.0.1 | zkserver1 | 2888:3888 |
| 172.0.0.2 | zkserver2 | 2888:3888 |
| 172.0.0.3 | zkserver3 | 2888:3888 |

在opt目录下将下载得到的zookeeper-3.4.12.tar.gz文件上传上去。

进入到该目录下：

```
cd  /opt/
1
```

执行解压命令：

```
tar -zxvf    zookeeper-3.4.12.tar.gz
1
```

## 1.三台服务器上都创建存放data文件及datalog文件夹

```
 mkdir  -p /opt/zookeeper/data
 mkdir   -p /opt/zookeeper/data/log
12
```

创建完毕情况验证

```
ll /opt/zookeeper
1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108192856666.png)

## 2. 创建myid文件

进入data文件夹下

```
cd /opt/zookeeper/data
1
```

分别将（可自行定义，内容仅供参考）：

```
vi /opt/zookeeper/data/myid
1
```

注意：编辑内容自己定义，只要和后面的配置文件server项对应上即可！！

将zkserver1机器上的/opt/zookeeper/data/myid文件的内容编辑为1
将zkserver2机器上的/opt/zookeeper/data/myid文件的内容编辑为2
将zkserver3机器上的/opt/zookeeper/data/myid文件的内容编辑为3

确认编辑完文件配置（三台都查看）：

```
cat /opt/zookeeper/data/myid
1
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193118355.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193122174.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193126781.png)

### 2.1备份初始配置文件样例并修改配置文件zoo.cfg

```
cp /opt/zookeeper-3.4.12/conf/zoo_sample.cfg  /opt/zookeeper-3.4.12/conf/zoo.cfg
mv /opt/zookeeper-3.4.12/conf/zoo_sample.cfg   /opt/zookeeper-3.4.12/conf/zoo_sample.cfg.bak 
12
```

把集群内的zookeeper的zoo.cfg配置文件都修改成一样的内容，主要是在末尾增加配置：

```
vi  /opt/zookeeper-3.4.12/conf/zoo.cfg
1
```

先删除 dataDir=/tmp/zookeeper这一行，在文件的末尾添加如下内容：

```
dataDir=/opt/zookeeper/data
dataLogDir=/opt/zookeeper/dataLog
server.1=172.0.0.1:2888:3888
server.2=172.0.0.2.163:2888:3888
server.3=172.0.0.3.169:2888:3888
12345
```

分别启动zookeeper服务：

```
/opt/zookeeper-3.4.12/bin/zkServer.sh start
1
```

查看状态

```
/opt/zookeeper-3.4.12/bin/zkServer.sh status
1
```

### **2.2部署成功状态**

zkserver1：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193418360.png)
zkserver2：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193427285.png)
zkserver3：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193435442.png)

## 3.模拟leader的节点挂掉。

好 ，我们来模拟leader的节点挂掉。
手动停止，我们的leader是server2.在server2上执行

```
/opt/zookeeper-3.4.12/bin/zkServer.sh stop
1
```

在查看状态
zkserver1：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193723778.png)

zkserver2（我们手动停止的节点）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190108193732540.png)
zkserver3（3节点自动接管了leader）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019010819374142.png)
搭建完毕！！！



！必须三台，如果报错先排查端口是否被占用，再看节点ip地址和myid是否配置正确，其他节点还没启动完成会报拒绝连接等!