# jQuery



## jQuery 介绍

官方介绍

> jQuery是一个快速小功能丰富的JavaScript库。它使如HTML文档遍历和操作，事件处理，动画和Ajax更简单和易于使用的API，跨越多种浏览器。结合的通用性扩展性，jQuery已经改变成了数百万人的方式编写JavaScript

参考文档

[jQuery在线中文文档](http://jquery.cuishifeng.cn/)

## jQuery的优势

jQuery作为JavaScript封装库，他的目的就是为了开发者使用

JavaScript主要功能有以下几点：

- 强大的选择器
- 像CSS那样访问和操作 DOM
- 修改CSS控制页面外观
- 事件处理更加容易
- 各种动画效果使用方便
- 让Ajax技术更加完美
- 基于JQuery 大量插件
- 自行扩展功能插件
- 出色的浏览器兼容
- 链式操作方式
- 隐式迭代
- 完善文档
- 开源

jQuery最大的优势，就是特别方便。比如模仿css获取DOM，比原生的JavaScript要方便太多。并且在多个css设置上的集合中处理非常舒服，而最常用的CSS功能又封装到单独方法，感觉非常有心最重要的是jQuery的代码兼容非常好，你不需要总是头疼着考虑不同浏览器的兼容问题

## jQuery下载和运行

CDN ，[下载](https://code.jquery.com/jquery-3.4.1.js)

```html
<script src="https://code.jquery.com/jquery-3.4.1.js"></script>
```

运行是否成功

```html
<!--引入jQuery包-->
<script src="https://code.jquery.com/jquery-3.4.1.js"></script>
<script>
   	//打印是否引入成功
	console.log(jQuery)
</script>
```

第一个jQuery代码

```html
<div id="app">
    云空
</div>
<!--引入jQuery包-->
<script src="https://code.jquery.com/jquery-3.4.1.js"></script>
<script>
	var oDiv = document.getElementById('app');
    console.log(oDiv)
    //js对象=>jQuery对象
    console.log(jQuery(oDiv));
    
    //console.log(jQuery);
    //jquery对象转换js对象
    console.log(jQuery('#app')[0]);
    console.log(('#app').get(0));
</script>
```

## jQuery基础核心

### 1.代码风格

在jQuery程序中，不管是页面元素的选择，内置的功能函数，都是美元符号$来开始的。而这个$就是jQuery当中最红要且独有的对象：jQuery对象，所以我们在页面元素选择或执行功能函数的时候可以这样写：

```js
$(function(){}) //执行一个匿名函数
$('#box'); //进行执行的ID元素选择
$('#box').css('color','red') //执行功能函数 css(css属性，css值)
```

由于$本身就是jQuery对象的缩写形式,那么也就是说上面的三行代码也可以写成如下形成：

```js
jQuery(function(){}) //执行一个匿名函数
jQuery('#box'); //进行执行的ID元素选择
jQuery('#box').css('color','red') //执行功能函数 css(css属性，css值)
console.log(jQuery === $);//true
```

并且，每次执行函数后，都会返回一个jQuery对象。如下：

```js
//链式编程 就是连续打点
$('#box').css('color','red').css('font-size','50px');
```

### 2.加载模式

> 我们在之前的代码一直在使用`$(function(){});`这段代码进行首尾包囊，那么为什么必须要包囊这代码呢？

- 我是jQuery库文件是在body元素之前加载，我们必须等所有DOM元素加载后，延迟支持DOM操作，否则就是无法获取到，使用 `document.ready()`,只需要等待DOM加载完成就执行。
- 我们的原生JavaScript也有延迟加载的方法onload,当网页内容全部加载完成后执行（例如图片等大文件未加载完成之前 JS功能处于假死状态）

onload和ready区别

| 区别       | winodw.onload                                              | $(document).ready()                                   |
| ---------- | ---------------------------------------------------------- | ----------------------------------------------------- |
| 执行  时机 | 必须等待网页全部加载完毕（包括图片等），然后在执行包囊代码 | 只需要等代码网页中DOM结构加载完毕，就能执行包囊的代码 |
| 执行  次数 | 只能执行一次，如果第二次，那么第一次的执行会被覆盖         | 可以执行多次，第N次都不会覆盖上一次                   |
| 简写  方案 | 无                                                         | `$(function(){})`                                     |

```html
<script>
	winodw.onload = function(){
        alert(1);
    }
    winodw.onload = function(){
        alert(2);
    }
    $(document).ready(function(){
        alert(1)
    })
      $(document).ready(function(){
        alert(2)
    })
</script>
```



### 3.对象互换及处理多个库之间的冲突

对象互换

首先我们先看一段代码

```js
alert($); //返回jQuery对象方法内部函数
alert($());//[object,object],返回jQuery对象
alert($('#box'));//[object object]
alert(document.getElementById('box'));//[object HTMLivElement] 返回原生DOM对象
```

如何进行转换呢？

jQuery想要获取原生DOM对象，可以这样处理

```js
$('#box').get(0);
//或者
$('#box')[0]
```

通过这个索引0可以看出jQuery是可以进行批量处理DOM的，这样可以在很多需要循环遍历的处理上更加得心应收。

当然要重新转换成为jQuery对象的话，只需要使用$()包囊原生对象就可以了

```js
var oBox = document.getElementById('box');
$(oBox);
```

多个库之间的冲突

当一个项目中进入多个第三方库的时候，由于没有命名空间的约束（命名空间就好比同一个目录下的文件夹一样，名字相同就会产生冲突），库与库之间发生冲突在所难免。

 jQuery只不过是DOM 操作为主的库，方便我们日常Web开发。但是时，我们的项目由更多特殊的功能需要引入其他的库，比如用户界面UI方面的库，游戏引擎方面的库等等一系里。

所以jQuery提供了一个方法：`jQuery.noConfilct()`;将$符所有权剔除。

```html
<script src="my.js"></script>
<script src="https://code.jquery.com/jquery-3.4.1.js"></script>
<script>
    //jQuery提供了一个解决多个库变量冲突的方法
	jQuery.noConfilct(); //将变量$控制权交给其他的js库
    console.log($);
    (function($){
        $(function(){
            $('#box').css('color','red');
        })
    })(jQuery)
	
</script>
```

## jQuery选择器

作用：是用于获取页面中的元素。jQuery的选择器的作用：选中当前的元素(返回一个jQuery对象)

### 基础选择器

模仿的是css选择器，只不过在使用jQuery选择器时，我们首先必须使用`$()`函数来包装我们的CSS规则。而CSS规则作为参数到jQuery对象内部后，在返回包含页面中对应元素的jQuery对象。随后可以进行节点操作，例如：`$('#box').css('color','red')`。

那么除了ID选择器之外，还有两种基本的选择器，分别为：元素标签名和类（class）：

| 选择器                  | 描述                                        | 返回     |
| ----------------------- | ------------------------------------------- | -------- |
| #id                     | 根据给定的ID匹配一个元素                    | 单个元素 |
| .class                  | 根据给定的类名匹配一个元素                  | 集合元素 |
| element                 | 根据给定的元素匹配一个元素（相对于tagName） | 集合元素 |
| *                       | 匹配所有元素                                | 集合元素 |
| select1,select2,select3 | 将每一个选择器匹配到的元素合并后一起返回    | 集合元素 |

我们可以采用jQuery核心自带的一个属性length来查看返回的元素个数

### 层次选择器

| 选择器                        | 描述                                          | 返回     |
| ----------------------------- | --------------------------------------------- | -------- |
| ancestor<br/>descendant(空格) | 选取ancestor 元素里所有的descendant(后代)元素 | 集合元素 |
| parent>child                  | 选取子元素                                    | 集合元素 |
| prev + next                   | 选取紧接在prev 元素后面的next元素             | 集合元素 |
| prev ~ sibings                | 选取 prev 元素之后的所有 siblings 元素        | 集合元素 |

代码示例

```html
<div>
    <p id='p1'></p>
    <ul>
        <li class="item1">张三</li>
        <li class="item2">李四</li>
        <li class="item3">王五</li>
    </ul>
</div>


<script src="https://code.jquery.com/jquery-3.4.1.js"></script>
<script>
    (function($){
        $(function(){
           //id获取元素 
           console.log($('#p1')); // <p id='p1'></p>
           //class获取元素 
           console.log($('.box')); 
           //标签获取元素
           console.log($('p'))
           //后代获取元素 
           console.log($('.box #p'));
           console.log($('.box ul li'))
           //子代获取元素
           console.log($('.box>ul>li'));
           //相邻的下一个元素  获取元素 
           console.log($('.box #p1'))
           // ~ 获取元素 
           console.log($('.box #p1'))
           // 组件
           console.log($('ul,li,p'))
        })
    })(jQuery)
</script>
```

### 基础过滤选择器

| 选择器         | 描述                              | 返回     |
| -------------- | --------------------------------- | -------- |
| :first         | 选取第一个元素                    | 单个元素 |
| :last          | 选取最后一个元素                  | 单个元素 |
| :not(selector) | 去除所有与给定选择器匹配的元素    | 集合元素 |
| :even          | 索引为偶数(索引从0开始)           | 集合元素 |
| :odd           | 索引为奇数(索引从0开始)           | 集合元素 |
| :eq(index)     | 索引等于index的元素(index从0开始) | 集合元素 |
| :gt(index)     | 索引大于 index                    | 集合元素 |
| :lt(index)     | 索引小于 index                    | 集合元素 |

### 内容过滤选择器

| 选择器           | 描述                                 | 返回     |
| ---------------- | ------------------------------------ | -------- |
| :contaions(text) | 查找文本中含有“text”的元素           | 集合元素 |
| :empty           | 匹配所有不包含子元素或者文本的空元素 | 集合元素 |
| :has(selector)   | 含有选择器所匹配的元素               | 集合元素 |
| :hidden          | 选取所有不可见的元素                 | 集合元素 |
| :visble          | 选取所有可见的元素                   | 集合元素 |

代码示例

```html
<div>
    <p id='p1'></p>
    <ul>
        <li class="item1">
        	<h3>张三</h3>
        </li>
        <li class="item2">李四</li>
        <li class="item3">王五</li>
    </ul>
</div>


<script src="https://code.jquery.com/jquery-3.4.1.js"></script>
<script>
    (function($){
        $(function(){
            //过滤选择器
            console.log($('ul li:first')); //获取是li集合中的第一个
            console.log($('ul li:last')); //获取是li集合的最后一个
            console.log($('ul li:not(.item2)'))//获取是除去li为(类名.item2)的li集合
            console.log($('ul li:even'));
            console.log($('ul li:odd'));
            //非常重要   text()方法是获取元素中的内容
            console.log($('ul li:eq(0)').text());
            console.log($('ul li:eq(2)').text());
            console.log($('ul li:get(0)').text());
            console.log($('ul li:lt(3)').text());
            
            //内容选择器
            console.log($('ul li:contaions(h3)'))
            
           
        })
    })(jQuery)
</script>
```

### 属性过滤择器

| 选择器               | 描述                       | 返回     | 示例                     |
| -------------------- | -------------------------- | -------- | ------------------------ |
| [attribute]          | 拥有此属性的元素           | 集合元素 | $("div[id]")             |
| [attribute = value]  | 属性的值为value的元素      | 集合元素 | $("div[title = test]")   |
| [attribute != value] | 属性的值不为value的元素    | 集合元素 | $("div[title != test]")  |
| [attribute ^= value] | 属性的值以value 开始的元素 | 集合元素 | $("div[tittle ^= test]") |

### 子元素过滤选择器

| 选择器 | 描述 | 返回 |      |
| ------ | ---- | ---- | ---- |
| :nth   |      |      |      |
|        |      |      |      |
|        |      |      |      |
|        |      |      |      |

### 表单过滤选择器

|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |

 

jQuery选择器完善的处理机制

- 如果元素不存在时，JS不会保存阻塞其他代码的运行
- $("#ID")或者其他选择器获取的永远是对象，即使网页没用此元素。使用jQuery检查某个元素是否存在要不能使用

```js
if($('#box')){
    //dosomething
    
}
```

而是根据元素是否有长度判断：

```js
if($('#box').length>0){
	//dosomething
}
```



## jQuery中的DOM操作

### jQuery的HTML DOM 操作

**增加节点**

| 方法          | 描述                                 | 示例                          |
| ------------- | ------------------------------------ | ----------------------------- |
| append()      | 向每个匹配的元素内部加内容           | $(A).append(B)将B             |
| appendTo()    | 将所有匹配的元素增加到指定原生中     | $(B).appendTo(A)将B追加到A中  |
| prepend()     | 向每个匹配的元素内部前置内部         | $(A).prepend(B)将B插入到A前面 |
| after()       | 在每个匹配的元素之后插入内容         | $(A).after(B)将B插入到A后     |
| insertAfter() | 将所有匹配的元素插入到指定元素的后面 | $(B).insertAfter(A)将B        |
|               |                                      |                               |

```html
<h3>小马哥<h3>
<div class='box'>
     
</div>  
<script>
	$(function(){
       //父子级操作
        //原生创建标签
        var h3Tag = document.createElement('h3');
        h3Tag.innerText = 'alex';
        //$('.box').append(h3Tag)    
        //字符串
        var html = '<h3>hello word<h3>'
        $('.box').append(html)
        
        //jq对象 如果网页中的元素，那么是一种移动现象 append appendTo 后置添加
        $('.box').append($('h3'));
        $('h3').css('color','red');
        //先创建在添加选中的父级
        $('<h4>老村长</h4>').appendTo('.box').css('color','green').click(function(){
            //原生对象
            console.log(this)
            //转换为jq对象
            console.log($(this).text());
        })
        //前置追加
        $(',box').prepend('<a href="#">百度一下</a>');
        $('<a href="#">百度一下2</a>').perpendTo('.box');
        
        
        //同级操作
        $('h3').after('<h1>wusir</h1>');
        $('<h2>老男人<h2>').inserAfter('h1')
        
        
        
	})    
</script>


```



**删除节点**

remove()

从DOM 中删除所有匹配的元素，传入的参数数用于根据jQuery 表达式来删除元素

```js

$('ul li:eq(1)').remove(); //获取第二哥 <li>元素节点后 将它从网页中删除
$li.appendTo("ul"); //把刚才删除的元素添加到<ul> 元素中复制代码

```

这个方法的返回值是一个指定已被删除的节点的引用，因此可以将其保存在一个变量中，可以还可以使用。

detach()

detach() 和delete() 一样，也是从DOM 中去掉所有匹配的元素，但是两者的区别是，这个方法不会把匹配的元素从jQuery对象中删除，去掉的元素的所有绑定的事件，附加的数据等都会保留下来。

empty()

清空元素中所有的后代节点。注意是清空元素内所有节点，并不清除选中的元素

```html
<div class="wrap">
    <button>
        按钮
    </button>
</div>
<div class="box">
    我是box
</div>
<script>
	$('button').click(function(){
    	alert(1);
        //即删除节点，又删除节点上的事件绑定
        //console.log($(this).remove);
        var btnJq  = $(this).remove()
        //仅仅删除了节点,事件保留
        //var btnJq = $(this).detach()
        $('.box').prepend(btnJq);
        //$(this).detach();
        
        //清空 div.box
        //$('.box').empty();
        //console.log($('.box').text());
        console.log($('.box').html());
        //input val()
        //清空
        $('.box').html('');
    })
</script>
```

https://www.bilibili.com/video/av69136894?p=9