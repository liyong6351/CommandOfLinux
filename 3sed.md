# 概览

sed是Linux的一种命令，用于处理String类型的数据，适合于log文件

## 1 UnderStand Sed Command

sed是一个不需要交互的命令，主要依赖于提供的规则对每一行进行编辑，使用方式如下:

```
$ sed option file
eg:
$ echo "Welcome to LikeGeeks page" | sed 's/page/website/'
```

sed 是按照行进行处理的，即使被处理的文件非常大，那么在处理过程中也会输出已经处理掉的数据，这就是他牛逼之处。awk也是一样的

## 2 Using Multiple sed Command in Command Line

如果在sed命令行中要嵌入多个条件，那么需要使用参数-e,条件之间使用;隔开

```
$ sed -e 's/This/That/; s/test/another test/' ./myfile
```

## 3 Reading Command From a File

可以将命令存储到一个命令文件中，使用参数-f指定需要运行的命令

```
$ sed -f mycommand myfile
```

## 4 Substituting Flags

如果不添加flag，那么在替换的时候，默认只替换第一个匹配的文档

```
$ cat myfile
This is a test and i like the test
this is a test and i don't like the test

$ sed 's/test/another test/' myfile
This is a another test and i like the test
this is a another test and i don't like the test
```

flag的撰写格式如下:

```
s/pattern/replacement/flags
其参数如下:
g 全局替换
A number,替换匹配的第n个,如果超出匹配范围则不处理
p 按照默认的替换，但输出原文件
w file，输出处理结果到另一个文件

$ sed 's/test/another test/w output' myfile
```

## 5 Replace Characters

如果需要在sed替换多个字符，那么可以使用以下命令:

```
$ sed 's/\/bin\/bash/\/bin\/csh/' /etc/passwd
```

看起来是不是很难看?可以按照以下途径改写

```
$ sed 's!/bin/bash!/bin/csh!' /etc/passwd
```

## 6 Liniting Sed

sed默认处理整个文件的问题，但可以限定处理的行数

```
$ sed '2s/test/another test/' myfile
$ sed '2,3s/test/another test/' myfile
$ sed '2,5s/test/another test/' myfile
$ sed '2,$s/test/another test/' myfile
```

这个也可以采用正则表达式进行处理

## 7 Delete Line

可以在sed中添加d标签引导在输出时删除指定的行，但是不会改变源数据

```
$ sed '3d' myfile
$ sed '1,3d' myfile
$ sed '3,$d' myfile
$ sed '/second/,/fourth/d' myfile
删除的是从匹配的second到匹配的fourth的数据
```

## 8 Insert and Append Text

可以使用i和a标签对输出的数据进行插入和添加工作

```
$ echo "Another test" | sed 'i\First test '
$ echo "Another test" | sed 'a\First test '
```

## 9 Modifying Lines

## 10 Transform Characters

## 11 Print Line Number

## 12 Read Data From File

## 13 Useful Example