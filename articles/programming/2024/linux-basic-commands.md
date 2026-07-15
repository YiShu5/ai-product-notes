# 【Linux篇】常用命令及操作技巧（基础篇）

> 原文：[【Linux篇】常用命令及操作技巧（基础篇）](https://blog.csdn.net/2302_79751907/article/details/141828988)  
> 作者：意疏｜许可：CC BY-SA 4.0

本篇整理 Linux 终端中最常用的文件、目录与文本操作命令。

## 获取帮助

```bash
man ls
ls --help
```

## 文件和目录

```bash
pwd                 # 显示当前目录
ls -lah             # 列出文件（含隐藏文件、详细信息）
cd /path/to/dir     # 进入目录
mkdir -p demo/src   # 创建多层目录
touch note.txt      # 创建空文件或更新时间戳
rm file.txt         # 删除文件
rm -r demo          # 递归删除目录（使用前务必确认路径）
```

绝对路径从根目录 `/` 开始；相对路径相对于当前目录。`.` 代表当前目录，`..` 代表上一级目录。

## 复制、移动与查看

```bash
cp source.txt backup.txt
mv old-name.txt new-name.txt
cat note.txt
more note.txt
grep "error" app.log
```

## 重定向与管道

```bash
echo "hello" > hello.txt       # 覆盖写入
echo "world" >> hello.txt      # 追加写入
grep "error" app.log | wc -l   # 把前一条命令的输出交给后一条
```

`*`、`?`、`[abc]` 等通配符可用于匹配文件名。对 `rm` 等破坏性命令，建议先用 `ls` 验证匹配结果，再执行删除。

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明。
