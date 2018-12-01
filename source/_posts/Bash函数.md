---
title: Bash函数
date: 2017-01-18 10:51:04
tags:  Linux
categories: Linux
---

Bash函数简述

一、什么是Bash函数

Bash不支持goto语句，可以用function实现程序流程跳转。
当前shell中一组组织在一起并被命名的命令。
比脚本的效率高，**一旦定义，就成为shell内存的一部分，可以随时被调用，不必从文件中读取。**
shell类似于编程语言的repl解释器，bash函数就是解释器的内置函数．

二、函数定义

两种定义方式：
1、函数名 +() + 定义
2、funciton + 函数名 + () + 定义，()可选
function func () {

    statements
        return 1；
}
第一个花括号两边的空格是必须的。

三、函数返回值

1、如果使用函数返回值，return只能返回一个整数（0~255），不能返回字符串，且返回值保存在$?变量中，不能直接赋值给其它变量
例如，下面获得函数返回值的写法是错误的

function func () { return 3; }
i=`func`
2、如果return没有指定参数，则是最后一行脚本的退出状态值

3、如果要将函数返回值赋值给一个变量，有两种方式：
a）用$?赋值

func
i=$?
b）在函数中，用echo打印返回值，再赋值

function func () { echo 3; }
i=`func`
四、函数参数

1、向函数传递的参数被当作位置参量来处理，在函数中是本地变量
2、函数参数用$1, $2 ,..., $n来表示，但和通过命令行传递给脚本的参数不同。调用方式如下：

func param1 param2
3、如果函数中要使用脚本的参数，只能将脚本的参数作为函数的参数传递给函数，例如，可以将脚本的第1个参数$1作为函数的第2个参数传给函数，那么函数则通过$2来访问脚本的第1个参数

$ function welcome { echo "Hi, $1 and $2"; }
$ welcome tom joe
Hi,tom and joe
$ set cb panda ; echo $*
cb panda
$ welcome tom joe
Hi,tome and joe
$ echo $1 $2
cb panda
五、函数中的变量和陷阱

1、在一个shell中的变量无局部和全局之分，随用随声明，无作用域的概念。例如，在一个if...fi块中定义的变量，出了这个块的作用域仍然有效。这也说明BASH不适合编写大的复杂的程序
2、和变量一样，函数内部的陷阱是全局的
3、函数中可以定义局部变量，出了函数无效，使用local来定义

func() {
    local count
        echo $count
}
六、函数调用

1、使用function只是定义函数，要执行函数中的命令必须在脚本中或命令行上调用函数，例如：$ func param1 param2
a) 将函数单独放入一个脚本里，再在命令行上执行脚本（直接执行，或使用.，或source），是不会执行函数里的命令的
b) 将函数单独放入一个脚本，然后执行，相当于在执行该脚本的shell环境中定义了该函数
例如：下面的命令只是在shell环境中定义函数，并不会调用函数
$ ./func_script.sh
或
$source ./func_script.sh

2、函数可以递归：函数可以自己调用自己，调用次数没有限制

3、函数中使用exit命令退出整个脚本。

七、常用命令

1、查看定义了哪些函数
$declare -f
$declare -F //只列出函数名

2、撤消函数定义
$unset func_name

3、将函数输出给子shell
$export -f func_name
