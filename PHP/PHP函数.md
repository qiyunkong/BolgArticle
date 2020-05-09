---
title: PHP函数
date: 2019-12-08 17:39:58
categories: PHP
tags:
- PHP	
---

官网：PHP函数的作用是将一些重复使用到的功能写在一个独立的代码块中，在需要时单独调用<!-- more -->

## 1.定义和调用函数

- 函数概念：将一些复合使用的功能写一个在一个独立代码块中，在需要时单独调用。
- 创建函数的基本语法格式为：

```php
function fun_name($str1,$stgr2,...$strn){
    fun_body; //执行的语句  fun_body是一个描述方法体的单词，不是PHP中的变量
    //fun_body; 可以写成输出名字的语句 
}
```

- 参数说明：
  - function:为<span style="color:#e67e22;">声明自定义函数时必须使用道关键字</span>。
  - fun_name:为<span style="color:#e67e22;">自定义函数的名称</span>。
  - $str1...$strn:为<span style="color:#e67e22;">函数的参数</span>
  - fun_body：为<span style="color:#e67e22;">自定义函数的主体，是功能实现部分</span>
- 函数的调用：当函数被定义好后，所要做的就是调用这个函数。调用函数的操作十分简单， 只需要<span style="color:#e67e22;">引用函数名并赋予正确的参数</span>即可完成函数的调用

```php
//语法
fun_name($str1,$stgr2,...$strn);
```

## 2.在函数传递参数

​	在调用函数时，需要向函数传递参数，被传入的参数称为实参，而函数定义的参数为形参。参数传递的方式有<span style="color:#e67e22;">按值传递、按引用传递</span>和<span style="color:#e67e22;">默认参数3种</span>

### 按值传递方式

```php
<?php
	function example($m){				//定义一个函数
		$m = $m*5+10;	
		echo "在函数内:\$m =".$m;		//输出形参的值
	}
	$m=1;
	example($m);						//传值:将$m的值传递给形参$m
	echo "<p>在函数外:\$m=$m<p>";		//实参的值没有发生变化，输出m=1

?>
```

### 按引用传递方式

```php
<?php
	function example2(&$m){				//定义一个函数
		$m = $m*5+10;	
		echo "在函数内:\$m =".$m;		//输出形参的值
	}
	$m2=1;
	example2($m2);							//传值:将$m的值传递给形参$m
	echo "<p>在函数外:\$m2= $m2 <p>";		//实参的值没有发生变化，输出m=1
?>
   
```

### 可选参参数方式

```php
<?php
	function values($price,$tax=0){				//定义一个函数
		$price = $price + ($price*$tax);	
		echo "价格:$price<br/>";		//输出形参的值
	}
	values(100,0.25);
	values(100);		
?>
```

## 3.在函数的返回值

​	如需让函数返回一个值，请使用 return 语句

```php
<?php
function add($x,$y)
{
    $total=$x+$y;
    return $total;
}
 
echo "1 + 16 = " . add(1,16);
?>
```

