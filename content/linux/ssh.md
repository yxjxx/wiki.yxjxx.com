---
title: "ssh"
date: 2015-08-23 14:46
---

Ubuntu自身默认是不带OpenSSH Server，而是只有OpenSSH Client。
(查看方法:`dpkg -l | grep openssh`

OpenSSH Server的安装方法：

`sudo apt-get install openssh-server`


当ubuntu防火墙开启时你可以 Ping 通, 但是无法 ssh 登录。

```
ufw enable  开户防火墙
ufw status  查看防火墙状态
ufw disable  禁用防火墙
```

重启远程主机的ssh服务

```
service ssh restart
```

##ssh related files' permission

| file/folder| permission |
| :-------- | --------:|
| .ssh/     |   700 |
| pub key   |   644 |
| pra key  |   600 |
| auth_keys |   600 |
| config    |   600 |
| known_hosts | 664 |

执行修改上述相关文件权限修改命令时不要加`sudo` 会改变用户组。

