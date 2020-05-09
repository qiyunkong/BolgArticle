---
title: PHP的表达式
date: 2019-12-05 17:39:58
categories: PHP
tags:
- PHP	

---

官网：表达式是构成PHP程序语言的基本元素，也是PHP最重要的组成元素。在PHP语言中，几乎 所写的任何对象都是表达式。 <!-- more -->

​	最基本的表达式形式：常量和变量。如$m=20，即表示将值20赋给变量$m

​	表达式是通过具体的代码来实现的，是多个符号集合起来组成的代码，而这些符号只是一些 对PHP解释程序有具体含义的最小单元。它们可以是<span style="color:#e67e22;">变量名</span>、<span style="color:#e67e22;">函数名</span>、<span style="color:#e67e22;">运算符</span>、<span style="color:#e67e22;">字符串</span>、<span style="color:#e67e22;">数值</span>和 <span style="color:#e67e22;">括号</span>等。如以下代码： 

```php
<?PHP  "fine" ; $a = "word" ;   ?> 
```

这就是由两个表达式组成的脚本，即fine和$a="word"。 

此外，还可以进行连续赋值，如：

```php
<?php $b = $a =5; ?>
```

 因为<span style="color:#e67e22;">PHP赋值操作的顺序是由右到左</span>的，所以变量$b和$a都被赋值5。

​	在PHP的代码中，<span style="color:#e67e22;">使用分号“;”来区分表达式</span>，表达式<span style="color:#e67e22;">也可以包含在括号内</span>。可以这样理解： 一个表达式再加上一个分号，就是一条PHP语句。应用表达式能够做很多事情，如调用一个数组、创建一个类、给变量赋值等。  注意：在编写程序时，应该注意表达式后面的分号“;”不要漏写。

<span style="color:red">注意：</span>在编写程序时，应该注意表达式后面的分号“;”不要漏写