# 特殊变量
在本章中，我们将详细讨论Unix中的特殊变量。在上一章中，我们了解了在变量名称中使用某些非字母数字字符时应注意的事项。这是因为这些字符用于特殊的Unix变量的名称中。这些变量保留用于特定功能。

例如，$字符表示当前shell的进程ID号或PID-

$ echo $$

上面的命令写入当前shell的PID-

29949
下表显示了一些可以在Shell脚本中使用的特殊变量-

序号变量与说明
1个
$ 0

当前脚本的文件名。

2
$ n

这些变量对应于调用脚本的参数。这里n是与参数位置相对应的正十进制数（第一个参数为$ 1，第二个参数为$ 2，依此类推）。

3
$＃

提供给脚本的参数数量。

4
$ *

所有参数都用双引号引起来。如果脚本收到两个参数，则$ *等效于$ 1 $ 2。

5
$ @

所有参数都单独用双引号引起来。如果脚本收到两个参数，则$ @等效于$ 1 $ 2。

6
$？

最后执行的命令的退出状态。

7
$$

当前shell的进程号。对于shell脚本，这是它们执行时的进程ID。

8
$！

最后一个后台命令的进程号。

命令行参数
命令行参数$ 1，$ 2，$ 3，... $ 9是位置参数，$ 0指向实际的命令，程序，shell脚本或函数，而$ 1，$ 2，$ 3，... $ 9作为参数。命令。

以下脚本使用与命令行相关的各种特殊变量-
```shell
＃！/ bin / sh

echo “文件名：$ 0”
echo“第一个参数：$ 1”
echo “第二个参数：$ 2”
echo “引用的值：$ @”
echo “引用的值：$ *”
echo“参数总数：$＃”
```
这是上述脚本的示例运行-
```shell 
$。/ test.sh Dong Chan
File name：./test.sh
第一个参数：Dong
第二参数：Chan
引用的值：DongChan
引用的值：DongChan
参数总数：2
```
## 特殊参数$ *和$ @
有一些特殊的参数允许一次访问所有命令行参数。 $ *和$ @的作用相同，除非用双引号“”引起来。

这两个参数都指定命令行参数。但是，“ $ *”特殊参数将整个列表作为一个参数，且之间使用空格，而“ $ @”特殊参数将整个列表视为一个参数，并将其分隔为单独的参数。

我们可以如下所示编写shell脚本，以使用$ *或$ @特殊参数处理未知数量的命令行参数-

```shell
#!/bin/sh

for TOKEN in $*
do
   echo $TOKEN
done
```
这是上述脚本的示例运行-
```shell
$./test.sh Dong Chan 10 Years Old
Dong
Chan
10
Years
Old
```
注意-在这里do ... done是一种循环，将在后续教程中进行介绍。

##  退出状态
$？变量表示上一个命令的退出状态。

退出状态是每个命令完成后返回的数值。通常，大多数命令如果成功则返回退出状态，如果失败则返回1。

某些命令出于特殊原因会返回其他退出状态。例如，某些命令区分错误的种类，并将根据故障的特定类型返回各种退出值。

以下是成功命令的示例-

```shell
$./test.sh Dong Chan
File Name : ./test.sh
First Parameter : Dong
Second Parameter : Chan
Quoted Values: Dong Chan
Quoted Values: Dong Chan
Total Number of Parameters : 2
$echo $?
0
$
```