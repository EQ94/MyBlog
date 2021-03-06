原文：[printf 格式化输出符号详细说明](http://blog.csdn.net/xiexievv/article/details/6831194)
* `%a`：浮点数、十六进制数字和p-记数法（C99）
* `%A`：浮点数、十六进制数字和p-记法（C99）
* `%c`：一个字符`char`
* `%C`：一个ISO宽字符
* `%d`：有符号十进制整数`int`
* `%ld,%Ld`：长整型数据`long`
* `%hd`：短整型数据
* `%e`：浮点数、e-记数法
* `%E`：浮点数、E-记数法
* `%f`：单精度浮点数（默认`float`），十进制记数法
* `%.nf`：这里`n`表示精确到小数位后`n`位，十进制记数法
* `%g`：根据数值不同自动选择`%f`或`%e`
* `%G`：根据数值不同自动选择`%f`或`%e`
* `%i`：有符号十进制数（与`%d`相同）
* `%o`：无符号八进制整数
* `%p`：指针
* `%s`：对应字符串`char*`（`%s == %hs == %hS`输出窄字符串）
* `%S`：对应宽字符串`WCAHR*`（`%ws == %S`输出宽字符串）
* `%u`：无符号十进制整数`unsigned int`
* `%x`：无符号十六进制整数（形式为`2f`）
* `%#x`：无符号十六进制整数（形式为`0x2f`）
* `%X`：无符号十六进制整数（形式为`2F`）
* `%#X`：无符号十六进制整数（形式为`0x2F`）
* `%%`：打印一个百分号
* `%lld`：用于`INT64`或者`long long`
* `%llu`：用于`UINT64`或者`unsigned long long`
* `%llx`：用于64位16进制数据

**说明：**

1. `%`：表示格式说明的起始符号，不可缺少
2. `-`：有`-`表示左对齐输出，如省略表示右对齐输出
3. `0`：有`0`表示指定空位填`0`，如省略表示指定空位不填
4. `m.n`：`m`指域宽，即对应的输出项在输出设备上所占的字符数；`n`指精度，用于说明输出的实型数的小数位数，未指定`n`时，隐含的精度为`n=6`位
5. `l,h`：`l`对整型指`long`型，对实型指`double`型；`h`用于将整型的格式字符修正为`short`型

**格式字符**

格式字符用以指定输出项的数据类型和输出格式。

* `d`格式：用来输出十进制整数。有以下几种用法：
    * `%d`：按整型数据的实际长度输出。
    * `%md`：`m`为指定的输出字段的宽度。如果数据的位数小于`m`，则左端补以空格，若大于`m`，则按实际位数输出。
* `o`格式：以无符号八进制形式输出整数。对长整型可以用`%lo`格式输出。同样也可以指定字段宽度用`%mo`格式输出。
* `x`格式：以无符号十六进制形式输出整数。对长整型可以用`%lx`格式输出。同样也可以指定字段宽度用`%mx`格式输出。
* `u`格式：以无符号十进制形式输出整数。对长整型可以用`%lu`格式输出。同样也可以指定字段宽度用`%mu`格式输出。
* `c`格式：输出一个字符。
* `s`格式：用来输出一个串。有以下几种用法：
    * `%s`：例如：`printf("%s", "CHINA")`输出字符串`CHINA`
    * `%ms`：输出的字符串占`m`列，如果字符串本身长度大于`m`，则突破获`m`的限制，将字符串全部输出。若串长小于`m`，则左补空格。
    * `%-ms`：如果串长小于`m`，则在`m`列范围内，字符串向左靠，右补空格。
    * `%m.ns`：输出占`m`列，但只取字符串中左端`n`个字符。这`n`个字符输出在`m`列的右侧，左补空格。
    * `%-m.ns`：其中`m,n`含义同上，`n`个字符输出在`m`列范围的左侧，右补空格。如果`n>m`，则自动取`n`值，即保证`n`个字符正常输出。
* `f`格式：用来输出实数（包括单、双精度），以小数形式输出。有以下几种用法：
    * `%f`：不指定宽度，整数部分全部输出并输出6位小数。
    * `%m.nf`：输出共占`m`列，其中有`n`位小数，若数值宽度小于`m`左端补空格。
    * `%-m.nf`：输出共占`m`列，其中有`n`位小数，若数值宽度小于`m`右端补空格。
* `e`格式：以指数形式输出实数。可用以下形式：
    * `%e`：数字部分（又称尾数）输出6位小数，指数部分占5位或4位。
    * `%m.ne,%-m.ne`：`m,n`和`-`字符含义与前相同。此处`n`指数据的数字部分的小数位数，`m`表示整个输出数据所占的宽度。
* `g`格式：自动选`f`格式或`e`格式中较短的一种输出，且不输出无意义的零。

**可变宽度参数**

对于`m.n`的格式还可以用如下方法表示：
```cpp
char ch[20];
printf("%*.*s\n",m,n,ch);
```
前边的`*`定义的是总的宽度，后边的定义的是输出的个数。分别对应外面的参数`m,n`。这种方法的好处是可以在语句之外对参数`m,n`赋值，从而控制输出格式。
