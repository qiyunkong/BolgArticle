---
title: PHP的数据类型
date: 2019-12-06 17:39:58
categories: PHP
tags:
- PHP	
---
官网：PHP是PHP的递归首字母缩写：Hypertext Preprocessor，一种用于创建动态和交互式HTML网页的脚本语言。当网站访问者打开页面时，服务器处理PHP命令，然后将结果发送到访问者的浏览器。<!-- more -->

<center><span style="color:#e67e22;">PHP的数据类型的概述:PHP一共支持8种原始类型</span></center>

| 4种标量类型            | 两种复合类型   | 两种特殊类型     |
| ---------------------- | -------------- | ---------------- |
| boolean（布尔型）      | array（数组）  | resource（资源） |
| integer（整型）        | object（对象） | NULL             |
| float/double（浮点型） |                |                  |
| string（字符串型）     |                |                  |

## 1.标量数据类型 

​	标量数据类型是数据结构中最基本的单元，只能存储一个数据。PHP中标量数据类型包括 4种，如下表所示

| 类型               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| boolean（布尔型）  | 这是最简单的类型。只有两个值，真（true）和假（false）        |
| string（字符串型） | 字符串就是连续的字符序列，可以是计算机所能表示的一切字 符的集合 |
| integer（整型）    | 整型数据类型只能包含整数。这些数据类型可以是正数或负数       |
| float（浮点型）    | 浮点数据类型用于存储数字，和整型不同的是它有小数位           |

### （1）布尔型（boolean）        

​	布尔型是PHP中较为常用的数据类型之一，它保存一个true值或者false值，其中true和false是 PHP的内部关键字。设定一个布尔型的变量，只需将true或者false赋值给变量即可。 

 	通常布尔型变量都是应用在条件或循环语句的表达式中。下面在if条件语句中判断变量$boo 中的值是否为true，如果为true，则输出“变量$boo为真!”，否则输出“变量$boo为假!!” 。 

```php
<?php
$x=true;
$y=false;
?>
```

<span style="color:red">注意：</span>在PHP中不是只有false值才为假的，在一些特殊情况下boolean值也被认为是false。这些特 殊情况为：<span style="color:#e67e22;">0、0.0、“0”、空白字符串（“”）、只声明没有赋值的数组</span>等。 

<span style="color:red">说明：</span>美元符号$是变量的标识符，<span style="color:#e67e22;">所有变量都是以$符开头的</span>，无论是声明变量还是调用变量，都 应使用$符

### （2）字符串型（string）        

​	字符串是连续的字符序列，由<span style="color:#e67e22;">数字、字母</span>和<span style="color:#e67e22;">符号</span>组成。字符串中的每个字符只占用一个字节。 在PHP中，有3种定义字符串的方式，分别是<span style="color:#e67e22;">单引号</span>（'）、<span style="color:#e67e22;">双引号</span>（"）和<span style="color:#e67e22;">界定符</span>（<<<）。单引 号和双引号是经常被使用的定义方式，

```php
<?php
	$a = '字符串'; 	//单引号
	$b = "字符串";		//单引号
?>
```

**单引号与双引号的区别**

​	两者的不同之处在于，双引号中所包含的变量会自动被替换成<span style="color:#e67e22;">实际数值</span>，而单引号中包含的变 量则按普通字符串输出。

​	下面的实例分别应用单引号和双引号来输出同一个变量，其输出结果完全不同，双引号输出的是变量的值，而单引号输出的是字符串“$i”。 

 	对转义字符的使用。<span style="color:#e67e22;">使用单引号时，只要对单引号</span>“‘”进行转义即可，但使用双引号（“） 时，还要注意“””、“$”等字符的使用。这些特殊字符都要通过转义符“\”来显示。常用 的转义字符如下表所示

| 转义字符           | 输出                                               |
| ------------------ | -------------------------------------------------- |
| \n                 | 换行（LF 或 ASCII 字符 0x0A（10））                |
| \r                 | 回车（CR 或 ASCII 字符 0x0D（13））                |
| \t                 | 水平制表符（HT 或 ASCII 字符 0x09（9））           |
| \\\                | 反斜杠                                             |
| \\$                | 美元符号                                           |
| \\'                | 单引号                                             |
| \\"                | 双引号                                             |
| \\[0-7]{1,3}       | 正则表达式序列匹配一个用八进制符号的字符，如\467   |
| \x[0-9A-Fa-f]{1,3} | 正则表达式序列匹配一个用十六进制符号的字符，如\x9f |

​	定界符（<<<）是从PHP4.0开始支持的。在使用时后接一个表示符，然后是字符串，最后是同样的标识符结束字符串。定界符的格式如下：

```php
$string = <<< str
要输出的字符串
str
```

​	其中str为指定的标识符。

<span style="color:red">注意：</span>结束标识符必须单独起一行，并且不允许有空格。在标识符前后其他符号或字符，也会发生错误。注释部分在练习时一定不要输入，否则将出现 “Parse error: parse error, unexpected T_SL in  路径 on line ..." 的错误提示

### （3）整型（integer）

​	整型数据类型只能包含整数。在32位的操作系统中，有效的范围是~2147483648～ +2147483647。整型数可以用十进制、八进制和十六进制来表示。如果用八进制，数字前面必须 加0，如果用十六进制，则需要加0x。

```php
<?php 
$x = 5985;
var_dump($x); //PHP var_dump() 函数返回变量的数据类型和值：
echo "<br>"; 
$x = -345; // 负数 
var_dump($x);
echo "<br>"; 
$x = 0x8C; // 十六进制数
var_dump($x);
echo "<br>";
$x = 047; // 八进制数
var_dump($x);
?>
```

<span style="color:red">注意：</span>如果在八进制中出现了非法数字（8和9），则后面的数字会被忽略掉 

<span style="color:red">注意：</span>如果给定的数值超出了int型所能表示的最大范围，将会被当作float型处理，这种情况称为 整数溢出。同样，如果表达式的最后运算结果超出了int型的范围，也会返回float型。 

### （4）浮点型（float）

 	浮点数据类型可以用来存储数字，也可以保存小数。它提供的精度比整数大得多。在32位的操作系 统中，有效的范围是1.7E-308～1.7E+308。在PHP 4.0以前的版本中，浮点型的标识为double， 也叫做双精度浮点数，两者没有区别。

**浮点型数据默认有两种书写格式：** 

```php

<?php 
$x = 10.365; //标准格式
var_dump($x);
echo "<br>"; 
$x = 2.4e3; //科学记数法格式
var_dump($x);
echo "<br>"; 
$x = 8E-5  //科学记数法格式
var_dump($x);
?>
```

<span style="color:red">注意：</span>浮点型的数值只是一个近似值，所以要尽量避免浮点型数值之间比较大小，因为最后的结果 往往是不准确的 

## 2.复合数据类型

​	复合数据类型包括两种，即数组和对象，如下表所示。

| 类型                                             | 说明                            |
| ------------------------------------------------ | ------------------------------- |
| arry(<span style="color:#e67e22;">数组</span>)   | 一组类型相同变量的集合          |
| object(<span style="color:#e67e22;">对象</span>) | 对象是类的实例，使用new命令创建 |

#### （1）数组（array）

​	数组是一组数据的集合，它把一系列数据组织起来，形成一个可操作的整体。数组中可以包括 很多数据，如<span style="color:#e67e22;">标量数据、数组、对象、资源</span>以及PHP中支持的其他语法结构等。 

​	  数组中的每个数据称为一个元素，元素包括<span style="color:#e67e22;">索引</span>（键名）和值两个部分。元素的索引可以由数 字或<span style="color:#e67e22;">字符串</span>组成，元素的值可以是多种数据类型

**定义数组的语法格式如下**

```php
//语法：$array = (‘value1’,‘ value2 ’……) 
$arr1 = array('This','is','a','example');  //实例
//语法：$array = array(key1 => value1, key2 => value2……) 
$arr2 = array(0 => 'php', 1=>'is', 'the' => 'the', 'str' => 'best ');  //实例
//语法： $array[key] = 'value' 
$arr3[0] = 'tmpname'; //实例
//其中，参数key是数组元素的下标，value是数组下标所对应的元素
```

<span style="color:#2ecc71;">提示:</span>声明数组后，数组中的元素个数还可以自由更改。只要给数组赋值，数组就会自动增加长度。 

#### （2）对象（object）

​	编程语言所应用到的方法有两种： <span style="color:#e67e22;">面向过程</span>和<span style="color:#e67e22;">面向对象</span>。在PHP中，用户 可以自由使用这两种方法,对象数据类型也可以用于存储数据。在PHP中，对象必须声明。首先，你必须使用class关键字声明类对象。类是可以包含属性和方法的结构。然后我们在类中定义数据类型，然后在实例化的类中使用数据类型：

```php
<?php
class Car
{
  var $color;
  function __construct($color="green") {
    $this->color = $color;
  }
  function what_color() {
    return $this->color;
  }
}
?>
//以上实例中PHP关键字this就是指向当前对象实例的指针，不指向任何其他对象或类。    
```



## 3、特殊数据类型

​	特殊数据类型包括资源和空值两种，如下表所示。 

| 类型                                               | 说明                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| resource(<span style="color:#e67e22;">资源</span>) | 是一种特殊变量，又叫做句柄，保存到外部资源的一个引用。资源是通过专门的函数来建立和使用的 |
| null(<span style="color:#e67e22;">口值</span>)     | 特殊的值，表示变量没有值，唯一的值就是null，                 |

#### （1）资源（resource）

​	资源类型是PHP 4引进的。关于资源的类型，可以参考PHP手册后面的附录，里面有详细的介 绍和说明。 

​	在使用资源时，系统会自动启用垃圾回收机制，释放不再使用的资源，避免内存消耗殆尽。因 此，资源很少需要手工释放。 

#### （2）空值（null）

​	空值，顾名思义，表示没有为该变量设置任何值，另外，空值（null）不区分大小写，null 和NULL效果是一样的。被赋予空值的情况有以下3种：还没有<span style="color:#e67e22;">赋任何值</span>、被赋值null、被unset() 函数处理过的变量。 

```php
<?php
echo "变量(\string1)直被赋值为null:";
$string1 = null;									//变量$string被赋空值
$string3 = "str";									//变量$string被赋值值str
if(isset($string1))									//判断$string是否被设置	
	echo "string1 = null";	
echo "<p>变量(\$string2)未被赋值 结果:";		
if(!isset($string2))								//判断$string2 是否被设置
	echo "string2 = null";
echo"<p>被unset()函数处理过的变量(\$string3) 结果:";
unset($string3);									//释放$string3
if(!isset($string3))
	echo "string3=null";							//判断$string3 是否被设置	
?>
```

<span style="color:red">说明：</span>is_null()函数是判断变量是否为null，该函数返回一个boolean型，如果变量为null，则返 回true，否则返回false。unset()函数用来销毁指定的变量。 

<span style="color:red">注意：</span>从PHP 4开始，unset()函数就不再有返回值，所以不要试图获取或输出unset()。 

## 4、转换数据类型 

​	虽然PHP是弱类型语言，但有时仍然需要用到类型转换。PHP中的类型转换和C语言一样，非常简单，只需在变量前加上用括号括起来的类型名称即可。允许转换的类型如下表所示。 

| 转换操作符 | 转换类型     | 举例                         |
| ---------- | ------------ | ---------------------------- |
| (boolean)  | 转换成布尔型 | (boolean)$num、(boolean)$str |
| (string)   | 转换成字符型 | (string)$boo、(string)$flo   |
| (integer)  | 转换成整型   | (integer)$boo、(integer)$str |
| (float)    | 转换成浮点型 | (float)$str、(float)$str     |
| (array)    | 转换成数组   | (array)$str                  |
| (object)   | 转换成对象   | (object)$str                 |

```php
<?php
$num = '3.1415926r*r';							//声明一个字符串变量
echo '使用(integer)操作符转换变量$num 类型:';			
echo (integer)$num;								//使用integer转换类型
echo '<p>';
echo '输出原始变量$num的值:'. $num;					//输出原始变量$num	
echo '<p>';												
echo '使用settype函数转换变量$num 类型:';				
echo settype($num,'integer');					  //使用settype函数转换 转换成功 返回值为1 否则 为0
echo '<p>';
echo '输出变量$num的值:' . $num;					 //输出原始变量$num
?>
```

<span style="color:red">注意：</span>在进行类型转换的过程中应该注意以下内容：

- 转换成boolean（布尔）型时，null、0和未赋值的变量或数组会被转换为false，其他的为真；
- 转换成integer（整型）时，布尔型的false转换为0，true转换为1，浮 点型的小数部分被舍去，字符型如果以数字开头就截取到非数字位，否则输出0。
-  类型转换还可以通过settype()函数来完成，该函数可以将指定的变量转换成指定的数据类型。 
- bool settype ( mixed var, string type )参数var为指定的变量，参数type为指定的类型，参数 type有7个可选值，即boolean、float、integer、array、null、object和string。如果转换成功则 返回true，否则返回false
-  当字符串转换为整型或浮点型时，如果字符串是以数字开头的，就会先把数字部分转换为整型，再舍去后面的字符串；如果数字中含有小数点，则会取到小数点前一位。 

## 5、检测数据类型

​	PHP还内置了检测数据类型的系列函数，可以对不同类型的数据进行检测，判断其是否属于 某个类型，如果符合则返回true，否则返回false。检测数据类型的函数如下表所示。 

| 函数                  | 检测类型                               | 举例                                   |
| --------------------- | -------------------------------------- | -------------------------------------- |
| is_bool               | 检查变量是否是布尔类型                 | is_bool(true)、is_bool(false)          |
| is_string             | 检查变量是否是字符串类型               | is_string('string')、is_string(1234)   |
| is_float 或 is_double | 检查变量是否为浮点类型                 | is_float(3.1415)、is_float('3.1415))   |
| is_integer 或 is_int  | 检查变量是否为整数                     | is_integer(34)、is_integer('34')       |
| is_null               | 检查变量是否为null                     | is_null(null)                          |
| is_array              | 检查变量是否为数组类型                 | is_array($arr)                         |
| is_object             | 检查变量是否是一个对象类型             | is_object($obj)                        |
| is_numeric            | 检查变量是否为数字或由数字组成的字符串 | is_numeric('5')、is_numeric('bccd110') |

