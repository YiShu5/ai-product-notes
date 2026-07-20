# 【C 语言篇】常考易错点大盘点：吃透这些，做题少踩坑

> 原文：[https://blog.csdn.net/2302_79751907/article/details/150220193](https://blog.csdn.net/2302_79751907/article/details/150220193)  
> 作者：意疏｜许可：CC BY-SA 4.0

## C语言常考及易错题整理

---

💬欢迎交流：在学习过程中如果你有任何疑问或想法，欢迎在评论区留言，我们可以共同探讨学习的内容。你的支持是我持续创作的动力！👍点赞、收藏与推荐：如果你觉得这篇文章对你有所帮助，请不要忘记点赞、收藏，并分享给更多的小伙伴！你们的鼓励是我不断进步的源泉！🚀推广给更多人：如果你认为这篇文章对你有帮助，欢迎分享给更多对C语言感兴趣的朋友，让我们一起进步，共同提升！

前言：

为帮助大家更好地掌握C语言核心知识点，本文整理了常考及易错题，涵盖变量作用域、宏定义、循环控制、编程实现等多个方面，每道题均附详细解析与优化代码，助力理解与巩固。

### 一、选择题

- 全局、局部和静态变量

题目：执行下面程序，正确的输出是：

```
int a = 5, b = 7;
void swap()
{
 int temp;
 temp = a;
 a = b;
 b = temp;
}
int main()
{ 
 int a = 3, b = 8; 
 swap();
 printf("%d,%d\n", a, b);
 return 0;
}
```

答案解析： 正确答案：3,8

swap函数操作的是全局变量a和b，但主函数中定义的a和b是局部变量。根据“局部变量优先”原则，main函数内的输出语句使用的是局部变量，因此结果为3,8。

- 静态局部变量

题目：如下函数的f(1)的值为：

```
int f(int num)
{
 static int count = 1;
 if(num >= 5)
 return num;
 num = num + count;
 count++;
 return f(num);
}
```

答案解析： 正确答案：7

静态局部变量count的生命周期贯穿函数多次调用，初始化仅执行一次。

- 第一次调用：num=1+1=2，count=2
- 第二次调用：num=2+2=4，count=3
- 第三次调用：num=4+3=7，满足num≥5，返回7
- 全局变量与循环

题目：以下程序的输出结果为：

```
#include <stdio.h>
int g;
void print_star()
{
 for (g = 5; g < 8; g++)
 printf("%c", '*');
 printf("\t");
}
int main()
{
 for (g = 5; g <= 8; g++)
 print_star();
 return 0;
}
```

答案解析： 正确答案：*** （3个星号+1个制表符）

全局变量g在main中初始化为5，第一次调用print_star()时：

- 循环执行g=5、6、7，输出3个*，g最终变为8
- 执行printf("\t")输出制表符 回到main后，g自增为9，不满足g≤8，循环结束，总输出为*** 。

4.#define与typedef

题目：test.c文件中定义的四个变量中，是指针类型的为【多选】：

```
#define PTR_INT int*
typedef int* int_ptr;
PTR_INT x, y;
int_ptr p, q;
```

答案解析： 正确答案：x、p、q

- 宏定义PTR_INT是文本替换，PTR_INT x,y;等价于int *x, y;，仅x为指针。
- typedef定义的int_ptr是独立类型，p和q均为指针。
- 宏替换计算

题目：以下程序结果输出是什么：

```
#include <stdio.h>
#define A 2
#define B A+1
#define SUM (B+1)*B/2
int main()
{
 printf("%d\n", SUM);
 return 0;
}
```

答案解析： 正确答案：8

宏替换仅做文本替换，SUM展开为(A+1+1)*A+1/2，代入A=2得：(2+1+1)*2 + 0 = 4*2 = 8（整数除法1/2=0）。

6.转义字符

题目：以下程序段输出结果是什么：

```
#include<stdio.h>
int main()
{ 
 char str[] = "\\123abc\123def\t"; 
 printf("%d\n", strlen(str)); 
 return 0;
}
```

答案解析： 正确答案：11

转义字符按1个字符计算：'\\'（1）、'\123'（1）、'a'（1）、'b'（1）、'c'（1）、'\123'（1）、'd'（1）、'e'（1）、'f'（1）、'\t'（1），共11个字符。

7.复合赋值操作符

题目：下面代码段的输出是：

```
#include <stdio.h>
int main()
{
 int num = 3; 
 printf("%d\n", (num += num -= num * num));
 return 0;
}
```

答案解析： 正确答案：-12

复合赋值从右向左计算：

- 先执行num -= num*num：num = 3 - 3*3 = -6
- 再执行num += -6：num = -6 + (-6) = -12

8.多层循环跳出

题目：下列跳出多层循环的做法正确的是【多选】：

A. 用return结束函数

```
void loop_func()
{
 for(int i=0;i<5;i++)
 {
 for(int j=0;j<5;j++)
 {
 if(i==2 && j==2)
 return; // 直接结束函数
 }
 }
}
```

B. 修改外层循环条件

```
for( int i = 0 ; i < MAX1 ; i ++ ) 
{
 for( int j = 0 ; j < MAX2 ; j ++ )
 {
 if( condition )
 {
 i = MAX1; // 使外层循环失效
 break;
 }
 }
}
```

C. 外层循环设判断条件

```
int flag = 0;
for( ; flag != 1 && condition2 ; )
{
 for( ; flag != 1 && condition3 ; )
 {
 if( condition1 )
 flag = 1 ;
 }
}
```

D. 外层循环后加break

```
int flag = 0;
for( ; condition2 ; )
{
 for( ; condition3 ; )
 {
 if( condition1 )
 flag = 1 ;
 }
 if( flag == 1 )
 break ;
}
```

答案解析： 正确答案：ABCD

四种方法均可实现多层循环跳出：

- A通过函数返回直接终止
- B通过修改外层变量使条件失效
- C、D通过标志位控制外层循环

9.循环执行次数

题目：执行下面的程序段，语句3的执行次数为：

```
for(i = 0; i <= n-1; i++) // (1)
 for(j = n; j > i; j--) // (2)
 statement; // (3)
```

答案解析： 正确答案：n(n+1)/2

外循环执行n次（i=0到i=n-1），内循环次数依次为n、n-1、…、1，总和为等差数列求和n+(n-1)+…+1 = n(n+1)/2。

10.while循环条件

题目：对于下面说法，正确的是：

```
int t=0;
while(printf("*"))
{
 t++;
 if (t<3)
 break;
}
```

A. 循环控制表达式与0等价 B. 循环控制表达式与’0’等价 C. 循环控制表达式不合法 D. 以上说法都不对

答案解析： 正确答案：B

printf("*")返回输出字符数1（非0，循环条件为真）。'0'的ASCII码为48（非0），与循环条件等价；0为假，故B正确。

11.字符输入统计

题目：以下不能统计一行输入字符数（不含回车）的程序段是：

A. n=0;while(ch=getchar()!='\n') n++; B. n=0;while(getchar()!='\n') n++; C. for(n=0;getchar()!='\n';n++); D. n=0;for(ch=getchar();ch!='\n';n++);

答案解析： 正确答案：D

D中for循环的初始化部分仅执行一次，ch只获取一次输入，若输入非回车则陷入死循环，无法统计。

12.switch语句穿透

题目：输入ADescriptor<回车>，程序运行结果是：

```
#include <stdio.h>
int main()
{
 char ch;
 int v0=0,v1=0,v2=0;
 do
 {
 switch(ch=getchar())
 {
 case'a':case'A':case'e':case'E':
 case'i':case'I':case'o':case'O':
 case'u':case'U':v1 += 1;
 default:v0+=1;v2+=1;
 }
 }while(ch!='\n');
 printf("v0=%d,v1=%d,v2=%d\n",v0,v1,v2);
 return 0;
}
```

答案解析： 正确答案：v0=12,v1=4,v2=12

输入共11个字符+回车（循环在回车时结束）。switch无break，匹配元音（A、e、i、o）时执行v1++后继续default；非元音直接执行default。最终v0=v2=12，v1=4。

13.结构体、浮点比较与数组赋值

题目：对于下面说法，正确的是：

A. struct X{short s;int i;char c;}的sizeof(X)等于成员大小之和 B. 可用a == 0.0判断double变量a是否为零 C. char a[14] = "Hello, world!";与char a[14]; a = "Hello, world!";效果相同 D. 以上说法都不对

答案解析： 正确答案：D

- A错误：结构体存在内存对齐，sizeof(X)大于成员之和
- B错误：浮点数有精度误差，不能直接用==判断
- C错误：数组名是常量，不能直接赋值

### 二、编程题

1.计算日期到天数转换

题目：根据输入的年、月、日，计算是这一年的第几天（保证日期合法）。

代码实现：

```
#include <stdio.h>
// 判断闰年：能被4整除且不能被100整除，或能被400整除
int is_leap(int year) {
 return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}
int main() {
 int year, month, day;
 // 每月天数（索引0未使用，方便月份直接对应）
 int days_in_month[] = {0,31,28,31,30,31,30,31,31,30,31,30,31};
 printf("请输入日期（格式：YYYY MM DD）：\n");
 while (scanf("%d %d %d", &year, &month, &day) == 3) {
 int total = day; // 累加当月天数
 // 闰年且月份>2时，2月多1天
 if (is_leap(year) && month > 2) {
 total += 1;
 } 
 // 累加之前所有月份的天数
 for (int i = 1; i < month; i++) {
 total += days_in_month[i];
 } 
 printf("%d\n", total);
 }
 return 0;
}
```

结果：

2.柯尼希定理（尼科彻斯定理）

题目：验证任何整数m的立方都可写成m个连续奇数之和，如3³=7+9+11，输入m并输出结果。

代码实现：

```
#include <stdio.h>
int main() {
 int m;
 while (scanf("%d", &m) == 1) {
 // 起始奇数公式：m*(m-1)+1
 int start = m * (m - 1) + 1;
 printf("%d", start); // 打印第一个奇数
 // 依次打印后续m-1个奇数（每次+2）
 for (int i = 1; i < m; i++) {
 start += 2;
 printf("+%d", start);
 }
 printf("\n");
 }
 return 0;
}
```

3.旋转数组的最小数字

题目：给定非降序数组的旋转数组（如[3,4,5,1,2]），求其中的最小值。

代码实现：

```
#include <stdio.h>
#include <limits.h>
int findMin(int* nums, int numsSize) {
 int left = 0, right = numsSize - 1;
 while (left < right) {
 int mid = left + (right - left) / 2;
 if (nums[mid] > nums[right]) {
 left = mid + 1;
 } else {
 right = mid;
 }
 }
 return nums[left];
}
int main() {
 int n;
 printf("请输入数组的长度：");
 scanf("%d", &n);
 int nums[n];
 printf("请输入旋转后的非降序数组元素（用空格分隔）：");
 for (int i = 0; i < n; i++) {
 scanf("%d", &nums[i]);
 }
 int min = findMin(nums, n);
 printf("数组中的最小值是：%d\n", min);
 return 0;
}
```

通过以上题目练习，可加深对C语言核心概念的理解，尤其注意变量作用域、宏特性、循环控制等易混淆点。编程题需注重逻辑梳理与边界处理，提升代码健壮性。

---

意气风发，漫卷疏狂学习是成长的阶梯，每一次的积累都将成为未来的助力。我希望通过持续的学习，不断汲取新知识，来改变自己的命运，并将成长的过程记录在我的博客中。如果我的博客能给您带来启发，如果您喜欢我的博客内容，请不吝点赞、评论和收藏，也欢迎您关注我的博客。 您的支持是我前行的动力。听说点赞会增加自己的运气，希望您每一天都能充满活力！愿您每一天都快乐，也欢迎您常来我的博客。我叫意疏，希望我们一起成长，共同进步。 我是意疏 下次见！
