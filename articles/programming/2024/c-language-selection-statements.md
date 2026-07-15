# C语言新手小白详细教程（3）选择语句

> 原文更新于 2024-07-28。  
> 原文：[C语言新手小白详细教程（3）选择语句](https://blog.csdn.net/2302_79751907/article/details/140648121)  
> 作者：意疏｜许可：CC BY-SA 4.0

程序的执行结构通常可以概括为三类：顺序结构、分支结构和循环结构。顺序结构按代码从上到下执行；分支结构会根据条件选择不同路径；循环结构则让一段逻辑重复执行。本篇聚焦分支结构。

![C 语言程序的三种基本结构](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/12-d3b1ac0c31ccbf627c6f27fb9351fae8.png)

## 1. if 语句

当条件为真时，执行花括号中的语句；条件为假时，跳过该代码块。

![if 语句格式](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/08-7c8e6a74a57ae672734401aea714782b.png)

```c
#include <stdio.h>

int main(void) {
    int number = 0;
    scanf("%d", &number);

    if (number > 0) {
        printf("输入的是正数\\n");
    }

    return 0;
}
```

`if` 后面的括号内是条件表达式。条件成立时执行语句块；不成立时程序继续往下运行。

![if 示例输出](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/01-03d8c07f5a305f4e04bf1b6c365403a6.png)

## 2. if...else 语句

如果需要在条件不成立时执行另一套逻辑，可以使用 `if...else`。

![if else 语句格式](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/10-97944582b0cbfa2f459c060ff5506ed8.png)

```c
#include <stdio.h>

int main(void) {
    int score = 0;
    scanf("%d", &score);

    if (score >= 60) {
        printf("及格\\n");
    } else {
        printf("不及格\\n");
    }

    return 0;
}
```

两条分支中只会执行其中一条：条件成立执行 `if`，否则执行 `else`。

![if else 示例输出](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/13-fae2ce41bcf90ade06ac3b7e8e1b77d9.png)

## 3. else if 语句

当判断条件不止两个时，可以用 `else if` 依次补充判断。

![else if 语句格式](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/11-a558db27bc6dd417135e18fefec15f6f.png)

```c
#include <stdio.h>

int main(void) {
    int score = 0;
    scanf("%d", &score);

    if (score >= 90) {
        printf("优秀\\n");
    } else if (score >= 60) {
        printf("及格\\n");
    } else {
        printf("不及格\\n");
    }

    return 0;
}
```

判断从上到下进行；遇到第一个成立的条件后，后续分支不会再继续判断。因此多条件判断时，要把范围更严格的条件放在前面。

![else if 示例输出](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/09-93ea9fa26973dd59e50242fbd5f151ce.png)

## 4. switch 语句

当同一个表达式需要和多个固定值比较时，`switch` 往往比一长串 `else if` 更清晰。

```c
switch (expression) {
    case constant1:
        /* 语句 */
        break;
    case constant2:
        /* 语句 */
        break;
    default:
        /* 所有 case 都不匹配时执行 */
        break;
}
```

![switch 基本结构](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/07-799d669b1edb493351e30edf822409f0.png)

```c
#include <stdio.h>

int main(void) {
    int day = 0;
    scanf("%d", &day);

    switch (day) {
        case 1:
            printf("星期一\\n");
            break;
        case 2:
            printf("星期二\\n");
            break;
        case 3:
            printf("星期三\\n");
            break;
        default:
            printf("请输入 1 到 3 之间的数字\\n");
            break;
    }

    return 0;
}
```

`break` 用来跳出整个 `switch`。如果某个 `case` 后面没有 `break`，程序会继续执行后续 `case` 的代码，这种现象叫作“贯穿”；初学时建议大多数分支都显式写上 `break`。

![带 default 的 switch 结构](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/06-636adcab6d6f7b3873e779b4298fb1af.png)

![break 的作用示意](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/02-1458d724775080e314edcd7ac7b00880.png)

![switch 示例输出](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/programming/2024/c-language-selection-statements/05-501957939fb5bb86cd686e28013f15bf.png)

## 小结

- 单个条件使用 `if`。
- 二选一使用 `if...else`。
- 多个范围条件使用 `else if`。
- 同一个值与多个常量匹配时使用 `switch`，并注意 `break` 与 `default`。

---

本文为作者 CSDN 原创文章的 Markdown 整理版，保留原文链接、作者署名与 CC BY-SA 4.0 许可说明；文章配图已迁移至 [ai-product-assets](https://github.com/YiShu5/ai-product-assets) 仓库。
