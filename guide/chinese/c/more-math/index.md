---
title: More math
localeTitle: 更多数学
---
# C中的更多数学

好的，所以你已经看过了基础知识。不过，在C中还有更多数学运算符，所以这里我们继续列举几个常用的。

## 运营顺序

看看下面的等式：

> 1 +（3-2）\* 5

如果我们只是从左到右阅读和计算，我们将取1，加3，减2，乘以5得到10。然而，这忽略了操作的顺序。我们应该先做（3-2），得到1，然后乘以5，再加1.这给出了6的答案。

就像常规数学一样，C有一个操作顺序。操作具有优先权，如果一个操作的优先级高于另一个操作，则首先计算优先级越高。使用括号可以增加该优先级，就像在普通数学中一样。

## 一元行动

一元操作是只有一个变量的操作。 C中有一些。

### 修复后和预修复操作员

在很多情况下你想要一个数字并且上升或下降1.对于这些情况，我们有post-fix和pre-fix运算符：

```C
1: a++; 
2: ++a; 
 
3: a--; 
4: --a; 
```

1和2处的示例都将a的值增加1。 3和4处的两个示例都将a的值减小1。但是，1与2不完全相同，3与4不完全相同。2和4中的运算符 ++ 叫预修复运算符，因为符号是前缀，在变量前被读取。这与我们在1和3的后修复操作符略有不同。预修复操作符先执行操作，然后再更新变量值。后修复操作符先返回值，然后再执行增量。

### 一元加减

在您习惯的常规数学中，您在数字或变量前面使用“ - ”，这使得数字或变量为负数。如果数字或变量已经为负数，则变为正数。

C做同样的事情：在数字或变量前放一个`-`以产生这种效果，如下所示：

```C
int number = -3; 
 number = -number; 
```

因此， `number`从负3开始，但随后变为正数，因为负数为正数。

## 按位运算

因为C是如前所述的低级别语言，所以您可以使用C访问各个二进制位（如果您选择利用它）。C中内置了一些二进制操作给予了我们这样做的能力。对于这些示例，我们将使用`a`和`b`作为变量。它们可以是任何类型的变量，因为所有变量都将以位表示，因此确切的数据类型对于这些变量无关紧要。

### 和

`c = a & b;`将执行按位AND。这意味着如果`a`的第一位和`b`的第一位都是1，则c的第一位将为1，否则为0。如果`a`和`b`的第二位都是1，则c的第二位将为1，否则为0。这种情况一直持续到所有比特都被读取过为止。

### 或

`c = a | b;将执行按位OR。如果`c`的第一比特是1，如果在任一`a`或`b`的第一比特是1；如果`a`和`b`的第一比特都是0，那么`c`的第一比特就是0。第二位、第三位如此类推。

### 否

`b = ~a;`将设置`b`到的一个补`a` ，这意味着`a`的任意一位是`b`的互补数；`a`的某个位置上的1会变成`b`相应位置上的0，而0会变成1。

### 异或

`c = a ^ b;`将执行按位异或。这意味着如果`a`的第一位或`b`的第一位为1，则`c`的第一位为1，但`a`和`b`不能同时为1。如果`a`和`b`的某个位置同时为1或0，那么`c`的相应位置会是0。依此类推。

### 位移

按位移位将取位并将它们移动到左侧或右侧的某些位置。例如，假设我们有一组位： `101110` 。当位移时，C执行算术移位。让我们用一张表来说明一点：

|位| | 1 | 2 | 3 | 4 | 5 | 6 | | ------- | --- | --- | --- | --- | --- | --- | --- | |之前| | 1 | 0 | 1 | 1 | 1 | 0 | |期间| 1 | 0 | 1 | 1 | 1 | 0 | | |之后| | 0 | 1 | 1 | 1 | 0 | 0 |

这是一个向左移动的算术按位移位。请注意，在左移位置，从位置1开始的最左边的1最终位于它可以适合的空间之外，因此它被移除了。在班次中，左侧出现一个开口，因此它充满了0。

现在让我们一起看一下算术位移：

|位| 1 | 2 | 3 | 4 | 5 | 6 | | | ------- | --- | --- | --- | --- | --- | --- | --- | |之前| 1 | 0 | 1 | 1 | 1 | 0 | | |期间| | 1 | 0 | 1 | 1 | 1 | 0 | |之后| 1 | 1 | 0 | 1 | 1 | 1 | |

请注意，这里的一个插槽在位置1处打开，但不是由0填充，而是由最重要的位填充。在这种情况下，这是1.如果在位置1开始的位为0，则间隙将填充0。

这是因为您的计算机上的数字是使用Two's Complement表示的，因此以这种方式移动不会使负数为正数。如果您对计算机如何使用二进制数据进行数学运算并表示数字感兴趣，那么Two's Complement值得更多阅读。

要执行左移，请使用`<<`运算符，如下所示：

```C
c = a << b; 
```

这将`a`向左移位`b`位，并将该结果设置为等于`c` 。

此示例将`a`向右移位`b`位，并将该结果设置为等于`c` 。

```C
c = a >> b; 
```

## 复合赋值运算符

有时您希望将变量增加一定值。在C中，您可以这样做：

```C
a = a + b; 
```

但是，这样的写法不够简练。这时，复合赋值运算符就派上了它的用场。以上的算法可以用复合赋值运算符更精炼地表达，如下所示：

```C
a += b; 
```

对于许多其他运算也存在这种情况。以下是给您的一个汇总表格：

短路|漫长的道路 ：--------------：|：------------： `a += b` | `a = a + b` `a -= b` | `a = a - b` `a *= b` | `a = a * b` `a /= b` | `a = a / b` `a %= b` | `a = a % b` `a &= b` | `a = a & b` `a ^= b` | `a = a ^ b` `a <<= b` | `a = a << b` `a >>= b` | `a = a >> b`

还有`|=` ，因为`|`会破坏桌子的格式，但它确实像所有这些其他操作一样，也是一种合理的运算。

## 铸件 (typecasting)

有时你不希望变量是一个数字，或者你想要一个整数变成浮点数，或类似的东西。这就是铸造的目的。

正如您从整数除法的讨论中回忆的那样，下面的示例的输入都是整数值，但它们的商是非整数，而C的printf语句只接受某种特定的变量类型，所以我们需要将它们的商转化成整数类型，才能被显示出来：

```C
#include <stdio.h> 
 
 int main(void) { 
    int a = 12; 
    int b = 5; 
 
    printf("a divided by b is %i", (int) a / b); 
 } 
```

其printf语句中的%i代表整数类型，(int) 这个操作就是铸件。铸件可以转换变量类型。

如果您想将a和b的商这个数字更准确地显示到屏幕上，你可以将这个商变成浮点数：

```C
#include <stdio.h> 
 
 int main(void) { 
    int a = 12; 
    int b = 5; 
 
    printf("a divided by b is %f", (float) a / b); 
 } 
```

现在它是一个浮点数，注意这里printf语句中的预留位是%f，是为浮点数准备的。所以这里将显示商为浮点数，该数字会保留一定的小数位数。

要将数字转换为`int` ，请使用`(int)`将其转换为`double` ，使用`(double)` ，其他同理。

## MATH.H

这就是所有内置的东西，但就像你可以`#include` stdio和stdbool一样，你可以包含一个名为`math.h`的库。该库具有各种有用的功能，适用于解决各种数学问题。如果你想要完整的功能列表，那么这个页面值得阅读[维基百科页面](https://en.wikipedia.org/wiki/C_mathematical_functions#Overview_of_functions) 。这里有一个关于如何使用`abs`的例子，这是他们列表中的第一个：

```C
a = abs(-1); 
```

`abs`计算传递给它的值的绝对值。在这种情况下，它收到-1，所以它会把它变成1， `a`将等于1。MATH.H库还有更多可以提供更多的功能，这就是你能够做指数，三角学，以及更多。

# 在你继续之前......

## 回顾

*   在C中有许多的数学运算符
*   C中存在操作顺序
*   可以使用括号并且它像常规数学一样工作以改变操作顺序
*   一元操作，这些操作只有一个变量：
*   post-fix和pre-fix运算符用于加1和减1
*   添加一个： `++a;`或者`a++;`
*   减去一个： - `--a`或'a--'
*   `-`可以放在变量或数字的前面，就像数学中的负数一样
*   也有一些按位操作
*   和用&完成
*   或者是用|完成
*   不是是用〜完成的
*   异或用^完成（异或不适用于C中的浮点型号）
*   所有非一元操作都存在复合赋值操作
*   a + = b与a = a + b相同，依此类推
*   铸件（typecasting）允许您在数据类型之间进行交换
*   MATH.H有更多的数学工具和函数可供使用

