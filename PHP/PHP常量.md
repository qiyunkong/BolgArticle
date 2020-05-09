---
title: PHP常量
date: 2019-12-03 18:39:58
categories: PHP
tags:
- PHP	

---

官网：PHP是PHP的递归首字母缩写：Hypertext Preprocessor，一种用于创建动态和交互式HTML网页的脚本语言。当网站访问者打开页面时，服务器处理PHP命令，然后将结果发送到访问者的浏览器。<!-- more -->

## 四、PHP常量

### 1.声明和使用常量

- **概述：**常量可以理解为值不变量。常量值被定义后，在脚本其他任何地方都不能改变
- **常量的组成规则：**一个常量英文字母、下滑线和数字组成、但是数字不能作为首字母出现。
- 在PHP使用define()函数来定义常量.

该函数的语法格式为:

```php
bool define ( string $name , mixed $value [, bool $case_insensitive = false ] )
```



| 参数           | 说明                                                |
| -------------- | --------------------------------------------------- |
| constant_name  | 比选参数，常量名称、标识字符                        |
| value          | 必须参数、常量的值                                  |
| case_sensitive | 可选参数，指定是否大小写敏感、设定为true,表示不敏感 |

- 获取常量的值有两种方法：一种是使用常量名直接获取值；另一种是使用constant()函数， constant()函数和直接使用常量名输出的效果是一样的，但函数可以动态地输出不同的常量， 在使用上要灵活方便得多。

函数的语法格式为：

```php
mixed constant(string const_name)
```

​	参数const_name为要获取常量的名称，也可为存储常量名的变量。如果成功则返回常量的值，否则提示错误信息常量没有被定义

- 使用defined()函数，来判断一个常量是否已经定义

函数的语法格式如下：

```php
 bool defined(string constant_name); 
```

参数constant_name为要获取常量的名称，成功则返回true，否则返回false 

```php
<?php
// 区分大小写的常量名
define("GREETING", "欢迎访问 qiyunkong.github.io");
echo GREETING;    // 输出 "欢迎访问  qiyunkong.github.io"
echo '<br>';
echo greeting;   // 输出 "greeting"
?>
<?php
// 不区分大小写的常量名
define("GREETING", "欢迎访问  qiyunkong.github.io", true);
echo greeting;  // 输出 "欢迎访问  qiyunkong.github.io"
?>
```

<span style="color:red">注意：</span>常量在定义后，默认是全局变量，可以在整个运行的脚本的任何地方使用。使用常量时，不能在常量名前添加**$** 符号，不然会将常量转换成新的未定义变量使用，会导致报错。

2、预定义常量

​	PHP中可以使用预定义常量获取PHP中的信息。常用的预定义常量如下表所示

| 常量名                 | 功能                                             |
| ---------------------- | ------------------------------------------------ |
| <u>__</u>FIE<u>__</u>  | 默认常量，PHP程序文件名                          |
| <u>__</u>LINE<u>__</u> | 默认常量，PHP程序行数                            |
| PHP<u>_</u>VERSION     | 内建常量，PHP程序的版本，如3.0.8<u>_</u>dev      |
| PHP<u>_</u>OS          | 内建常量，执行PHP解析器的操作系统名称，如Windows |
| TRUE                   | 该常量是一个真值（true）                         |
| FALSE                  | 该常量是一个假值（false）                        |
| NULL                   | 一个null值                                       |
| E<u>_</u>ERROR         | 该常量指到最近的错误处                           |
| E<u>_</u>WARNING       | 该常量指到最近的警告处                           |
| E<u>_</u>PARSE         | 该常量指到解析语法有潜在问题处                   |
| E<u>_</u>NOTICE        | 该常量为发生不寻常处的提示但不一定是错误处       |

<span style="color:red">注意：</span><u>__</u>FIE<u>__</u>和<u>__</u>LINE<u>__</u>中的“__”是两条下划线，而不是一条“_”。 

<span style="color:red">说明：</span>表中以E_开头的预定义常量，是PHP的错误调试部分。如需详细了解，请参考 error_ reporting()函数。 

 