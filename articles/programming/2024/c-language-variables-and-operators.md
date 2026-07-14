# C语言新手小白详细教程（2）变量与运算符

> 原文发布于 2024-07-07，更新于 2024-07-28。  
> 原文：[C语言新手小白详细教程（2）变量与运算符](https://blog.csdn.net/2302_79751907/article/details/140249137)  
> 作者：意疏｜许可：CC BY-SA 4.0

这一篇接着环境搭建继续学习 C 语言的基础：程序如何存储数据、如何从终端接收输入，以及怎样用运算符让数据参与计算和判断。

## 1. 从 Hello World 开始

```c
#include <stdio.h>

int main(void) {
    printf("Hello, world!\\n");
    return 0;
}
```

- `#include <stdio.h>`：引入标准输入输出库，`printf` 和 `scanf` 都在这里声明。
- `main`：程序的入口函数。
- `\\n`：换行。
- `return 0`：通常表示程序正常结束。

## 2. 常见数据类型

C 语言中的变量在声明时需要先写清类型。最常用的是：

| 类型 | 含义 | 示例 |
| --- | --- | --- |
| `char` | 单个字符或小整数 | `'A'` |
| `int` | 整数 | `18` |
| `float` | 单精度小数 | `3.14f` |
| `double` | 双精度小数 | `3.1415926` |
| `void` | 无类型/无返回值 | `void print_info(void)` |

不同编译器、不同平台下类型的字节数可能不同。写程序时可以通过 `sizeof` 查看真实大小：

```c
#include <stdio.h>

int main(void) {
    printf("int: %zu bytes\\n", sizeof(int));
    printf("double: %zu bytes\\n", sizeof(double));
    return 0;
}
```

## 3. 变量与常量

变量可以理解为一个有名字的存储位置。声明后可以赋值，也可以在运行中改变值：

```c
int age = 18;
float price = 99.9f;
char grade = 'A';

age = 19;
```

命名建议以字母或下划线开头，只包含字母、数字和下划线；不能使用关键字，例如 `int`、`return`。

不希望值被修改时，可以用 `const`：

```c
const double PI = 3.1415926;
```

## 4. 输出：printf

`printf` 用于把内容输出到屏幕。常见格式控制符如下：

| 格式 | 输出内容 |
| --- | --- |
| `%d` | `int` 整数 |
| `%c` | 单个字符 |
| `%f` | 浮点数 |
| `%.2f` | 保留两位小数的浮点数 |

```c
#include <stdio.h>

int main(void) {
    int count = 3;
    char initial = 'Y';
    double score = 95.678;

    printf("count = %d\\n", count);
    printf("initial = %c\\n", initial);
    printf("score = %.2f\\n", score);
    return 0;
}
```

## 5. 输入：scanf

`scanf` 用于从标准输入读取数据。对于普通变量，要传入变量的地址，因此前面要加 `&`：

```c
#include <stdio.h>

int main(void) {
    int age;
    float height;

    printf("请输入年龄和身高：");
    scanf("%d %f", &age, &height);

    printf("年龄：%d，身高：%.1f\\n", age, height);
    return 0;
}
```

初学阶段要特别留意两点：格式控制符要和变量类型一致；`scanf` 返回值可用于判断是否成功读取到预期数量的数据。

## 6. 算术运算符

常用算术运算包括 `+`、`-`、`*`、`/`、`%`。其中 `%` 是取余，只能用于整数。

```c
int a = 7;
int b = 3;

printf("%d\\n", a + b);  // 10
printf("%d\\n", a - b);  // 4
printf("%d\\n", a * b);  // 21
printf("%d\\n", a / b);  // 2：整数除法
printf("%d\\n", a % b);  // 1
```

`++` 与 `--` 分别表示自增和自减。前置形式先变化后使用，后置形式先使用后变化：

```c
int i = 5;
printf("%d\\n", i++); // 输出 5，随后 i 变为 6
printf("%d\\n", ++i); // i 先变为 7，再输出 7
```

## 7. 关系、逻辑和条件运算符

关系运算符用于比较：`>`、`>=`、`<`、`<=`、`==`、`!=`。条件成立时表达式结果为真，否则为假。

逻辑运算符用于组合条件：

- `&&`：并且；两边都为真才为真。
- `||`：或者；任意一边为真就为真。
- `!`：非；把真假取反。

```c
int age = 20;
int has_ticket = 1;

if (age >= 18 && has_ticket) {
    printf("可以入场\\n");
}
```

三目运算符可以在简单的二选一场景中替代 `if...else`：

```c
int score = 85;
const char *result = score >= 60 ? "及格" : "不及格";
printf("%s\\n", result);
```

## 8. 赋值运算符与优先级

除 `=` 以外，C 语言还提供了简写形式：`+=`、`-=`、`*=`、`/=`、`%=`。

```c
int total = 10;
total += 5;  // 等价于 total = total + 5;
```

表达式同时出现多种运算符时，需要注意优先级。最简单、也最可靠的做法是：不确定时加括号，让意图清楚地写在代码里。

```c
int result = (a + b) * 2;
```

## 小结

这一篇的重点是：用合适的数据类型声明变量；用 `printf` 输出、`scanf` 输入；熟悉算术、关系、逻辑、三目和赋值运算符。下一步可以把这些基本元素放进分支和循环结构中，开始编写能根据条件作出不同响应的程序。

---

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明。
