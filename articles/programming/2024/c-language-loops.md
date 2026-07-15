# C语言新手小白详细教程（4）循环语句

> 原文：[C语言新手小白详细教程（4）循环语句](https://blog.csdn.net/2302_79751907/article/details/140648056)  
> 作者：意疏｜许可：CC BY-SA 4.0

循环用于在条件满足时重复执行同一段代码。C 语言常用的循环有 `while`、`do...while` 和 `for`，配合 `break`、`continue` 可以控制循环过程。

## while

`while` 会先判断条件；条件为真才执行循环体，因此循环体可能一次也不执行。

```c
int sum = 0;
int i = 1;
while (i <= 100) {
    sum += i;
    i++;
}
printf("1 到 100 的和是：%d\n", sum);
```

![while 循环示例](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-loops/12-22cf159f3cd9427d8068b5918dbd6cba.png)

## do...while

`do...while` 先执行一次循环体，再判断条件，因此循环体至少会执行一次。

```c
int i = 1;
do {
    printf("%d ", i);
    i++;
} while (i <= 5);
```

## for

`for (初始化; 条件; 更新)` 将循环控制集中在一行，适合循环次数或控制变量清晰的场景。

```c
int sum = 0;
for (int i = 1; i <= 100; i++) {
    sum += i;
}
```

## break 与 continue

`break` 立即结束整个循环；`continue` 只跳过本轮剩余语句，进入下一轮。

```c
for (int i = 0; i < 10; i++) {
    if (i == 5) break;
    printf("%d ", i);
}

for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) continue;
    printf("%d ", i);
}
```

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明。
