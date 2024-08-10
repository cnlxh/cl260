# 处理CL260课程环境问题

```text
作者：李晓辉

联系方式：

1. 微信：Lxh_Chat

2. 邮箱：939958092@qq.com
```

`CL260-RHCS5.0-1.r2021120708`的环境有些bug需要处理才能正常使用，具体如下：

# 设置foundation的时间

这一步在foundation上完成

需要设置时间为`2024-07-05`之前的时间，不然容器镜像无法拉取，我这里设置一个`2023-09-09`

```bash
timedatectl set-ntp 0
timedatectl set-time '2023-09-09'
systemctl disable chronyd --now
```

# 设置foundation软件仓库

这一步在foundation上完成

必须设置以下仓库，不然无法安装诸如`ceph-common`等软件

```bash
mkdir /content/rhel8.4/x86_64/rhel8-additional
mount -o loop \
/content/rhcs5.0/x86_64/isos/rhel-8.4-x86_64-additional-202110061700.iso \
/content/rhel8.4/x86_64/rhel8-additional
sed -i '$ a /content/rhcs5.0/x86_64/isos/rhel-8.4-x86_64-additional-202110061700.iso /content/rhel8.4/x86_64/rhel8-additional iso9660 loop,ro 0 0' /etc/fstab
systemctl daemon-reload
ssh root@classroom 'systemctl restart httpd' 
```

# 设置Clienta软件仓库

这一步在Clienta上完成

这一步主要是修复`awscli`的客户端安装以及`lab start api-s3`这个操作

```bash
cat > /etc/yum.repos.d/aws.repo <<-'EOF'
[epel-8-for-x86_64-rpms]
baseurl = http://content.example.com/rhel8.4/x86_64/rhel8-additional/epel-8-for-x86_64-rpms
enabled = true
gpgcheck = false
name = awscli
EOF
```


