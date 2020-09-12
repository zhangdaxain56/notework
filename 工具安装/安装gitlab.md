#### 安装gitlab

1，安装依赖
yum install -y curl policycoreutils-python openssh-server

#### centos8没有policycoreutils-python yum源，不用管

2，启动ssh并设置为开机自启动
`systemctl enable sshd`

```
systemctl start sshd
```

3,添加http服务到firewalld,pemmanent表示永久生效，若不加--permanent系统下次启动后就会失效
`systemctl start firewalld`

```
firewall-cmd --permanent --add-service=http
systemctl reload firewalld
```

4,启动postfix
`systemctl enable postfix`

```
systemctl start postfix
```

5,下载gitlab

此处可到官网下载：

`wget https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el8/gitlab-ce-12.10.1-ce.0.el8.x86_64.rpm`

6,安装
`rpm -i gitlab-ce-10.0.0-ce.0.el7.x86_64.rpm`