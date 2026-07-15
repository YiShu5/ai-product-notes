# 【Linux篇】常用命令及操作技巧（进阶篇 - 下）

> 原文：[【Linux篇】常用命令及操作技巧（进阶篇 - 下）](https://blog.csdn.net/2302_79751907/article/details/142533124)  
> 作者：意疏｜许可：CC BY-SA 4.0

本篇继续 Linux 命令与操作技巧，重点说明超级用户与权限管理中的常见操作。

## 超级用户与 sudo

超级用户 `root` 拥有系统最高权限。日常操作不建议长期直接使用 root，而应在确实需要管理权限时通过 `sudo` 临时提权：

```bash
sudo apt update
sudo systemctl restart ssh
```

`sudo` 会根据系统配置检查当前用户是否有执行权限。不要把不可信命令直接放在 `sudo` 前执行，也不要随意把普通账号加入管理员组。

## 常见权限检查

```bash
ls -l file.txt
stat file.txt
```

`ls -l` 可快速查看文件权限、属主与所属组。例如：

```text
-rw-r--r-- 1 user group 1234 file.txt
```

其中前三位权限属于文件所有者，中间三位属于同组用户，最后三位属于其他用户。

## 实操原则

- 先确认当前用户：`whoami`、`id`。
- 修改权限前先查看现状：`ls -l`。
- 对目录递归执行 `chmod` 或 `chown` 前，先检查目标路径。
- 仅在需要时使用 `sudo`，避免以 root 身份执行日常操作。

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明。
