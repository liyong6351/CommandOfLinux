# 概览

本章全面而详细的学习awk

<pre>
awk是处理文本文件的一个应用程序，几乎所有 Linux 系统都自带这个程序。
它依次处理文件的每一行，并读取里面的每一个字段。对于日志、CSV 那样的每行格式相同的文本文件，awk可能是最方便的工具。
</pre>

## 1 awk基本用法

* 格式  awk [动作] 文件名
* 示例  awk '{print $0}' demo.txt

> 在awk中$0表示当前行，上述命令是打印demo.txt的每一行。
> awk会根据空格和制表符，将每一行分成若干字段，依次用$1、$2、$3代表第一个字段、第二个字段、第三个字段等等。
> -F 参数可以指定这个文件字段的分隔符，例如

* awk -F ':' '{print $1}' /etc/passwd

## 2 awk变量

> 除了$ + 数字表示某个字段，awk还提供其他一些变量。
> 变量NF表示当前行有多少个字段，因此$NF就代表最后一个字段。$(NF-1)代表倒数第二个字段。

*  awk -F ':' '{print $1 $NF}' demo.txt

> 变量NR表示当前处理的是第几行。

* awk -F ':' '{print NR ") " $1}' demo.txt

|内置变量名|说明|
|:--|:--|
|FILENAME|文件名|
|FS|字段分隔符，默认是空格和制表符|
|RS|行分隔符，默认是空格|
|OFS|输出字段的分隔符，用于打印时分割字段|
|ORS|输出行分隔符，用于打印时分割字段
|OFMT|数字的输出格式，默认为%.6g|

## 3 函数

* awk还提供了一些内置函数，方便对原始数据的处理。

* awk -F ':' '{ print toupper($1) }' demo.txt

* 连接: https://www.gnu.org/software/gawk/manual/html_node/Built_002din.html#Built_002din

|函数|说明|
|:-|:-|
|tolower|转换为小写|
|toupper|转换为大写|
|length|返回字段的长度|
|substr|返回子字符串|
|sin|正弦|
|cos|余弦|
|sqrt|平方根|
|rand|随机数|

## 4 条件

* 格式: awk '条件 动作' 文件名

* awk -F ':' '/usr/ {print $1}' demo.txt
上面代码中，print命令前面是一个正则表达式，只输出包含usr的行。

## 5 条件

