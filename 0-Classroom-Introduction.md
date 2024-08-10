```text
作者：李晓辉

联系方式：

1. 微信：Lxh_Chat

2. 邮箱：939958092@qq.com
```

# 课堂环境介绍

![](https://gitee.com/cnlxh/cl260/raw/master/images/classroom/Classroom-Architecture.png)



所有虚拟机共享外部网络 172.25.250.0/24，其网关为 172.25.250.254 (`bastion`)。外部网络 DNS 和容器注册表服务由 `utility` 提供。



其他用于实践练习的学员虚拟机包括 `clienta`、`clientb`、`serverc`、`serverd`、`servere`、`serverf` 和 `serverg`。所有系统都在 `lab.example.com` DNS 域内。

所有学员计算机系统都有一个标准用户帐户 `student`，其密码为 `student`。所有学员系统的 `root` 密码都是 `redhat`。



# 虚拟机介绍

| 计算机名称                       | IP 地址          | 角色                  |
| --------------------------- | -------------- | ------------------- |
| workstation.lab.example.com | 172.25.250.9   | 学员图形工作站             |
| clienta.lab.example.com     | 172.25.250.10  | 客户端“A”作为集群客户端和管理节点  |
| clientb.lab.example.com     | 172.25.250.11  | 客户端“B”集群客户端         |
| serverc.lab.example.com     | 172.25.250.12  | 服务器“C”集群存储节点        |
| serverd.lab.example.com     | 172.25.250.13  | 服务器“D”集群存储节点        |
| servere.lab.example.com     | 172.25.250.14  | 服务器“E”集群存储节点        |
| serverf.lab.example.com     | 172.25.250.15  | 服务器“F”第二集群存储节点      |
| serverg.lab.example.com     | 172.25.250.16  | 服务器“G”备用集群存储节点      |
| utility.lab.example.com     | 172.25.250.17  | 实用程序服务，如 DNS 和容器注册表 |
| classroom.example.com       | 172.25.254.254 | 课堂资料和内容服务器          |
| bastion.lab.example.com     | 172.25.250.254 | 将虚拟机链接到中央服务器的路由器    |



`classroom` 服务器使用以下URL来提供特定练习的课程内容： 

- `content.example.com` 

- `materials.example.com` 。

# 管理存储集群

课堂环境中安装了两个 Ceph 存储集群。

- Ceph 主要集群由 `serverc`、`serverd` 和 `servere` 组成。

- Ceph 次要集群由 `serverf` 组成。`clienta.lab.example.com` 服务器已安装 `cephadm` 容器，并且具有管理 Ceph 主要集群所需的配置。`serverf.lab.example.com` 服务器已安装 `cephadm` 容器，并且具有管理 Ceph 次要集群所需的配置。


