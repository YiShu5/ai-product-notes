# 【Linux篇】常用命令及操作技巧（进阶篇 - 上）

> 原文：[【Linux篇】常用命令及操作技巧（进阶篇 - 上）](https://blog.csdn.net/2302_79751907/article/details/142327429)  
> 作者：意疏｜许可：CC BY-SA 4.0

本篇聚焦 Linux 的远程管理、网络信息、SSH 与用户权限操作。涉及系统和权限的命令会直接影响机器状态，执行前应确认当前环境与目标对象。

## 远程管理与系统状态

```bash
shutdown -h now       # 立即关机
reboot                # 重启
```

## 网卡与 IP 地址

```bash
ip addr
ip link
ping -c 4 8.8.8.8
```

`ip addr` 用于查看网卡、IPv4/IPv6 地址和网卡状态；排查网络时也可结合 `ping` 检查连通性。

## SSH 基础

```bash
ssh user@host
scp local.txt user@host:/home/user/
```

SSH 用于安全远程登录，`scp` 可以在本机与远程主机之间复制文件。生产环境应优先使用密钥认证，并妥善管理私钥权限。

## 用户与权限

```bash
whoami
id
chmod 644 file.txt
chown user:group file.txt
```

- `whoami`：查看当前用户名。
- `id`：查看用户 ID、所属组等信息。
- `chmod`：修改权限位。
- `chown`：修改所有者和所属组。

权限通常由“所有者、所属组、其他用户”三组读 (`r`)、写 (`w`)、执行 (`x`) 权限组成。对权限和属主的修改应遵循最小权限原则。

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明。
