# Less

Less是css预处理器

less 是一种动态样式语言,属于css预处理器的范畴，它扩展css语言

增加了变量 Mixin 函数等特性 使css更容易维护和扩展

less官网 链接---》[](http://lesscss.cn/)

## less在浏览器端使用

引入js编译less

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/less.js/2.5.3/less.min.js"></script>
```

**注意：要放在html标签的下面**

引入style

```html
<style type="text/less"></style>
```

**注意： 是type="text/less" 而不是type="text/css"**

## less中的注释

1. 以//开头的注释,不会被编译到css文件中
2. 以/**/包裹的注释会被编译到css文件中

```less
/*这是想暴漏的注释*/
//这是见不得人的事情
```



## less中的变量

使用@来声明一个:@pink:pink;

1. 作为普通属性值只来使用,直接使用@pink
2. 作为选择器和属性名：#@{selector的值}的形式
3. 作为URL:@{url}
4. 变量的延迟加载

### **css属性为变量**

```less
@m:margin;
*{
	@{m}: 0;
	padding: 0;
}
```

​	**注意:是需要花括号---> { }**

### **css属性值为变量**

```less
@red:red;
div{
	color:@red;
}
```

### **css选择器为变量**

```less
@selector:#wrap;
@{selector}{
    width:200px;
    height:200px;
    margin:0 auto;
}
```

​	**注意:是需要花括号---> { } 插值**

### **url为变量**

```less
@url:"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1578810576593&di=76f195bd03c130f8c74f3d446a3a8416&imgtype=0&src=http%3A%2F%2Fn.sinaimg.cn%2Fsports%2Ftransform%2F20170611%2FPOgi-fyfzfyz3141496.jpg";

.box{
	background-image:url(@url);
}
```

**变量的延迟加载**

less中

```less
@var:0;
#box{
    @var:1;
    one:@var;
    .box{
        @var:2;
        two:@var;
        @var:3;
    }
    .box2{
        three:@var;
        @var:5;
    }
}
```

css中

```css
#box{
	one:1;
}
#box .box{
	two:3;
}
#box .box2{
	@var:5;
}
```



## less中嵌套规则

1. 基本嵌套规则（与html嵌套相似）
2. &的使用

## less后代选择器代码

```less
/*我是less 写法*/
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
    
	.box{
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		margin: auto;
		width: 300px;
		height: 300px;
		background-color: #0000FF;
	}
}

```

1. **当直接嵌套写 会被解析成 （外：.wrap）和(内：.box)中间有个空格**
2. **a{ b{} }  解析为a{样式} a b{ 样式 }**   

解析成css代码

```css
/*解析出的css代码*/
.wrap {
  position: relative;
  width: 600px;
  height: 600px;
  margin: 0 auto;
  transition: 0.5s;
  border: 1px solid red;
}
.wrap .box {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 300px;
  height: 300px;
  background-color: #0000FF;
}
```

## less（伪类）或者（子、兄）选择器

```less
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
	&>.box{
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		margin: auto;
		width: 300px;
		height: 300px;
		background-color: #0000FF;
		&:hover{
			background-color: red;
		}
		&:after{
			content: "";
			position: absolute;
			top:0;
			left: 0;
			width: 100px;
			height:100px;
			background-color: #333333;
		}
	}
}
```

1. **&这个符号作用是 连接css选择器的符号**
2. **css 选择器符号有很多 比如 冒号(:) 大于号(>) 加号(+) 等....**

编译成css代码

```css
/*less嵌套规则*/
* {
  margin: 0 ;
  padding: 0 ;
}
.wrap {
  position: relative;
  width: 600px;
  height: 600px;
  margin: 0 auto;
  transition: 0.5s;
  border: 1px solid red;
}
.wrap > .box {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 300px;
  height: 300px;
  background-color: #0000FF;
}
.wrap > .box:hover {
  background-color: red;
}
.wrap > .box:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100px;
  height: 100px;
  background-color: #333333;
}

```

## less中混合方法

​	官方解释：混合就是将一个系列属性从一个规则引入到另一个规则集的方法

​	自我理解：混合蛋白是一种可以大量减少重复代码量的使用

1. 普通混合	（可以被编译到css代码中）
2. 不带输出的混合 （不带输出的混合就是不编译到css代码中）
3. 带参数的混合 （Mixins混合）
4. 带参数并且有默认值的混合
5. 带多个参数的混合
6. 命名参数
7. 匹配模式
8. arguments变量

### 普通混合

```less
/*less嵌套规则*/
*{
	margin: 0 ;
	padding: 0 ;
}
/*定义混合的居中代码*/
.centered{
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
	color: #0000FF;
}
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
	&>.box{
		/*使用混合 start*/
		.centered;
		/*使用混合 end*/
		position: absolute;
		width: 300px;
		height: 300px;
		background-color: #0000FF;
		&:hover{
			background-color: red;
			color: #0000FF;
			font-weight: 700;
		}
		&:after{
			content: "";
			position: absolute;
			.centered;
			width: 100px;
			height:100px;
			background-color: #333333;
		}
	}
}
```

​	**注意	定混合是以点（.）开头**

编译成css代码

```less
/*less嵌套规则*/
* {
  margin: 0 ;
  padding: 0 ;
}
/*居中代码*/
.centered {
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  color: #0000FF;
}
.wrap {
  position: relative;
  width: 600px;
  height: 600px;
  margin: 0 auto;
  transition: 0.5s;
  border: 1px solid red;
}
.wrap > .box {
  /*使用混合 start*/
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  color: #0000FF;
  /*使用混合 end*/
  position: absolute;
  width: 300px;
  height: 300px;
  background-color: #0000FF;
}
.wrap > .box:hover {
  background-color: red;
  color: #0000FF;
  font-weight: 700;
}
.wrap > .box:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  color: #0000FF;
  width: 100px;
  height: 100px;
  background-color: #333333;
}

```

​	**补充：我们会看到编译出了的css代码中会一个[ .centered{ css样式} ]这个css选择器的样式代码，混合的目的已尽达到了，但是这个[ .centered{ css样式} ]是多余的，我们想在编译中不让它解析出了，要给less代码修改，就是在混合命名后面加上一对括号**

### 不带输出的混合

```less
/*less嵌套规则*/
*{
	margin: 0 ;
	padding: 0 ;
}
/*定义混合的居中代码*/
.centered(){
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
	color: #0000FF;
}
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
	&>.box{
		/*使用混合 start*/
		.centered();
		/*使用混合 end*/
		position: absolute;
		width: 300px;
		height: 300px;
		background-color: #0000FF;
		&:hover{
			background-color: red;
			color: #0000FF;
			font-weight: 700;
		}
		&:after{
			content: "";
			position: absolute;
			.centered();
			width: 100px;
			height:100px;
			background-color: #333333;
		}
	}
}
```

​	这样就不会导致编译出来的css代码有些是多余的，防止原生的css代码量过大

### 带参数的混合

```less
/*less嵌套规则*/
*{
	margin: 0 ;
	padding: 0 ;
}
/*定义混合的居中代码 可以传三个参数的 宽度 高度 颜色*/
.centered(@w,@h,@c){
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
	width: @w;
	height:@h;
	background-color: @c;
}
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
	&>.box{
		/*使用混合 start*/
		.centered(300px,300px,red);
		/*使用混合 end*/
		&:hover{
			background-color: red;
		}
		&:after{
			content: "";
			.centered(100px,100px,#ccc);
		}
	}
}
```

编译成css代码

```css
/*less嵌套规则*/
* {
  margin: 0 ;
  padding: 0 ;
}
/*定义混合的居中代码 可以传三个参数的 宽度 高度 颜色*/
.wrap {
  position: relative;
  width: 600px;
  height: 600px;
  margin: 0 auto;
  transition: 0.5s;
  border: 1px solid red;
}
.wrap > .box {
  /*使用混合 start*/
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 300px;
  height: 300px;
  background-color: red;
  /*使用混合 end*/
}
.wrap > .box:hover {
  background-color: red;
}
.wrap > .box:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 100px;
  height: 100px;
  background-color: #ccc;
}
```

### 带参数并且有默认值的混合

```less
/*less嵌套规则*/
*{
	margin: 0 ;
	padding: 0 ;
}
/*定义混合的居中代码 默认值 300px 300px blue*/
.centered(@w:300px,@h:300px,@c:blue){
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
	width: @w;
	height:@h;
	background-color: @c;
}
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
	&>.box{
		/*使用混合 start*/
		.centered();
		/*使用混合 end*/
		&:hover{
			background-color: red;
		}
		&:after{
			content: "";
			.centered(100px,100px,#ccc);
		}
	}
}
```

编译成css代码

```css
/*less嵌套规则*/
* {
  margin: 0 ;
  padding: 0 ;
}
/*定义混合的居中代码*/
.wrap {
  position: relative;
  width: 600px;
  height: 600px;
  margin: 0 auto;
  transition: 0.5s;
  border: 1px solid red;
}
.wrap > .box {
  /*使用混合 start*/
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 300px;
  height: 300px;
  background-color: blue;
  /*使用混合 end*/
}
.wrap > .box:hover {
  background-color: red;
}
.wrap > .box:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 100px;
  height: 100px;
  background-color: #ccc;
}

```

## less命名参数

```less
/*less嵌套规则*/
*{
	margin: 0 ;
	padding: 0 ;
}
/*定义混合的居中代码 默认值 300px 300px blue*/
.centered(@w:300px,@h:300px,@c:blue){
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	margin: auto;
	width: @w;
	height:@h;
	background-color: @c;
}
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
	&>.box{
		/*使用混合 start*/
		.centered();
		/*使用混合 end*/
		&:hover{
			background-color: red;
		}
		&:after{
			content: "";
			.centered(@w:50px,@h:50px,@c:#fff);
		}
	}
}
```

编译成css代码

```css
/*less嵌套规则*/
* {
  margin: 0 ;
  padding: 0 ;
}
/*定义混合的居中代码 默认值 300px 300px blue*/
.wrap {
  position: relative;
  width: 600px;
  height: 600px;
  margin: 0 auto;
  transition: 0.5s;
  border: 1px solid red;
}
.wrap > .box {
  /*使用混合 start*/
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 300px;
  height: 300px;
  background-color: blue;
  /*使用混合 end*/
}
.wrap > .box:hover {
  background-color: red;
}
.wrap > .box:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
  width: 50px;
  height: 50px;
  background-color: #fff;
}

```

## less匹配模式

html

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title></title>
    </head>
    <body>
        <div class="wrap">
            <div class="box"></div>
        </div>
    </body>
</html>
```

第一个less文件（自定义less库）

```less
.triangle(@_){
    width: 0;
    height: 0;
   	overflow:hidden;
}
.triangle(L,@w,@c){
    border-width: @w;
    border-style:dashed solid dashed dashed;
    border-color:transparent @c transparent transparent;
}
.triangle(R,@w,@c){
    border-width: @w;
    border-style:dashed  dashed dashed solid;
    border-color:transparent transparent transparent @c;
}
.triangle(T,@w,@c){
    border-width: @w;
    border-style:dashed  dashed solid dashed;
    border-color:transparent  transparent @c transparent;
}
.triangle(B,@w,@c){
    border-width: @w;
    border-style:solid dashed dashed dashed;
    border-color:@c transparent transparent transparent;
}
```

第二个less文件

```less
@import "./index2.less"; //导入第一less文件
*{
	margin: 0 ;
	padding: 0 ;
}
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
	.box2{
		.triangle(R,200px,red);
	}
}
```

​	**补充：@import是导入文件 	语法：@import "路径"**

编译成css代码

```css
.wrap{
	position: relative;
	width: 600px;
	height: 600px;
	margin: 0 auto;
	transition: .5s;
	border:  1px solid red;
}
.wrap .box2 {
  border-width: 200px;
  border-style: dashed  dashed dashed solid;
  border-color: transparent transparent transparent red;
}
```

## less 中的arguments变量

```less
.border(@1,@2,@3){
    border:@arguments;
}
.box{
    .border(1px,solid,black)
}
```

编译成css代码

```css
.box{
	border:1px solid black;
}
```

## less中的计算(wmv)

```less
width:(100 + 100px);
```

## less中的继承

less 文件

```less
.juzhong{
    position:absolute;
    top:0;
    left:0;
    bottom:0;
    right:0;
    margin:auto;
}
.juzhong:hover{
  	background-color:red;
}
```

less 文件2

```less
@import "mixin/juzhong-extend.less";
#wrap{
	position:relative;
	width:300px;
	height:300px;
    border:1px solid;
    margin:0 auto;
    .inner{
        &:extend(.juzhong all);
        &:nth-child(1){
            width:100px;
            height:100px;
             background-color:pink;
        }
        &:nth-child(2){
            width:50px;
            height:50px;
            background-color:yellow;
        }
    }
}
```

## less中的避免编译

