# C语言新手小白详细教程（6）初步理解函数

> 原文：[C语言新手小白详细教程（6）初步理解函数](https://blog.csdn.net/2302_79751907/article/details/140945943)  
> 作者：意疏｜许可：CC BY-SA 4.0

函数把一段可复用的逻辑封装起来，让程序更容易阅读、修改和复用。

## 定义与调用

```c
#include <stdio.h>

void say_hello(void) {
    printf("Hello!\n");
}

int main(void) {
    say_hello();
    return 0;
}
```

函数由返回类型、函数名、参数列表和函数体组成。`void` 表示函数不返回值。

## 形参与实参

定义函数时括号内的变量叫形式参数；调用函数时传入的值叫实际参数。

```c
int add(int a, int b) {
    return a + b;
}

int result = add(3, 5);
```

`a`、`b` 是形参，`3`、`5` 是实参。C 语言的普通参数传递默认是值传递：函数内修改形参，不会直接改变调用方的变量。

## return 与函数声明

`return` 用于结束函数并把结果返回给调用处。若函数定义放在调用之后，需要先声明函数：

```c
int add(int a, int b);

int main(void) {
    printf("%d\n", add(2, 3));
}

int add(int a, int b) {
    return a + b;
}
```

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明。
