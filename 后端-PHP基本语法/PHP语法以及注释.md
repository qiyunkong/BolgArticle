---
title: PHP语法
date: 2019-12-02 17:39:58
categories: PHP
tags:
- PHP	
---

官网:HTML（中文:超文本标记语言）是用于在Internet(指的是IE浏览器)上显示Web页面的主要标记语言。网页由HTML组成，用于通过Web浏览器显示文本，图像或其他资源。HTML文件的文件扩展名为.htm或.html

<!-- more -->

## 一、PHP标记风格

​	 PHP和其他几种Web语言一样，都是使用<span style="color:#e67e22;">一对标记对将PHP代码部分包含起来</span>，以便和html 代码相区分。PHP一共**支持**<span style="color:#e67e22;">4种</span>**标记风格**

### XML 风格

```php
<?php
    echo "这是XML风格的标记";
?>
```

​	XML风格的标记是本书所使用的标记，也是推荐使用的标记，服务器不能禁用。该风格的标 记在XML、XHTML中都可以使用。 

### ASP风格

```php
<%  
	echo '这是ASP风格的标记'; 
%> 
```

### 脚本风格

```php+HTML
<script language="PHP">
     echo '这是脚本风格的标记';
</script>
```

### 简短风格 

```php
<? echo '这是简短风格的标记'; ?> 
```

 	如果要使用简短风格和ASP风格，需要在php.ini中对其进行配置。该文件在系统盘Windows目录下，如操作系统在C盘，那么该文件的位置就是 C:\Windows\php.ini。

 	如果用户用的是AppServ安装包，那么通过选择“开始<span style="color:#e67e22">”/“程序” /appServ/Configuration Server/PHP Edit the php.ini configuration File命令，</span>也可以<span style="color:#e67e22">打开 php.ini文件，然后将short_open_tag和asp_tags都设置为ON，重启Apache服务器</span>即可。  

## 二、PHP注释的应用和风格

​	注释即代码的解释和说明，一般<span style="color:#e67e22">放到代码的上方或代码的尾部</span>（放尾部时，代码和注释之间 以<tab>键进行分隔，以方便程序阅读），用来<span style="color:#e67e22">说明代码或函数的编写人、用途、时间</span>等。<span style="color:#e67e22">注释 不会影响到程序的执行</span>，因为在执行时，注释部分会被解释器忽略不计 

### C++风格的单行注释（//）

```php
<?php
  echo '使用C++风格'; //这就是C++风格 echo 关键字是输出的意思
?>
```

### C风格的多行注释（/*....*/）

```php
<?php
	/*风格的多行注释*/
	echo '只会看到这句话。';
?>
```

<span style="color:red">注意：</span>多行注释是不允许进行嵌套的。

Shell 风格的注释（#）

```php
<?php 
	echo '这是Shell脚本风格的注释';  
	#这里的内容是看不到的 
?> 
```

<span style="color:red">注意：</span>在单行注释中的内容不要出现“?>” 标志，因为解释器会认为PHP脚本结束，而 去执行“?>”后面的代码 

