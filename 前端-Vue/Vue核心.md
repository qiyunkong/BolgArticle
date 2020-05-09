# vue

## 入手的vue

  vue官网引入vue的cdn

```vue
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

vue的书写

​	解析vue元素对象的属性中的数据  	vue中想让变量解析到dom上需要加 {{变量}}

```vue
<div id="app">
    {{a}}
</div>
<!--引入vue cdn--->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
	new Vue({
        el:'#app', //使用Vue特性 选择元素 el --> Elements （元素）：选择器
        data:{ //data 是存放在组件的数据 
            a:1,
            b:2,
            arr:[1,2,3]
        }
        
    })
</script>
```

​	vue的数据都存放**data**这个大的对象中

​	使用vue绑定事件 <https://learning.dcloud.io/#/?vid=10>

```vue
	<!-- 
		vue中想让变量解析到dom上
		需要加 {{变量}} 插值表达式
		v-on:事件名="事件处理函数名"
		v-on是vue的一个指令 可以简化为@
		v-on:click=事件处理函数 等价 @click=事件处理函数
	-->
	<div id="app">
		{{a}}
		<button v-on:click="handleClick">点击改变data选择数据</button>
	</div>


	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<script type="text/javascript">
		new Vue({
			el:'#app', //使用Vue特性的范围 在那个节点内容可以使用vue的特性
			//data 是
			data:{ //存在组件的数据 为根组件
				a:1,
				b:2,
				arr:[1,2,3],
				obj:{
					name:'heaven',
					age:29
				}
			},

			methods:{ //存放事件处理函数
				handleClick:function(){
					console.log("我被点击了")
					this.a++;
				}
			}
		})

```

​	vue的绑定的事件处理函数都存放在**methods**中

​	多个事件绑定

```vue
<div @click.capture="handleParent">
    Parent
    <div @click="handleSon">
        Son
        <div @click="handleGrandSon">
            Grandson
        </div>
    </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script type="text/javascript">	
	new Vue({
			el:'#app', //使用Vue特性的范围 在那个节点内容可以使用vue的特性
			//data 是
			data:{ //存在组件的数据 为根组件
				a:1,
				b:2,
				arr:[1,2,3],
				obj:{
					name:'yunkong',
					age:29
				},
			},
			methods:{ //存放事件处理函数
				handleParent(){
					alert("parent");
				},
				handleSon(){
					alert("son");
				},
				handleGrandSon(){
					alert("grandson");
				},
			}
		})

</script>
```

## vue 的事件

| 事件名 | 作用                 |
| ------ | -------------------- |
| keyup  | 按键事件（鼠标抬起） |
|        |                      |
|        |                      |

事件的修饰符	修饰符语法： 一个英文点加一个单词

| .stop        | 阻止事件冒泡 e.stopPropagtion |
| :----------- | ----------------------------- |
| **.capture** | **是事件捕获**                |
| **.pervent** | **阻止默认的行为**            |
| **.once**    | **一次处理性函数**            |

按键的修饰符

| **.up**    | 只能是上键 才会触发事件 |
| ---------- | ----------------------- |
| **.enter** | **按下回车键**          |

## vue的数据回收

v-model  该指令可以把vue中的数据和表单的数据绑定在一块（双向数据邦定）

***1.普通的文本框/文本域中   收集的是文本框的输入数据***

```vue
<div id="app">
	文本框：<input type="text" v-model.trim="text">
     文本域：<textarea v-model="textArea"></textarea>
     <button @click="handleClick">点击收集数据</button>
</div>

<script>
	let vm = new Vue({
        el:'#app',
        data:{
            text:'', //收集文本框输入数据
            textArea:'' //收集文本域的输入数据
        },
        methods:{
            handleClick(){
               console.log('文本框的数据是${this.text}')
            }
            
        }

    })
</script>
```

**2.*单选按钮              收集的是单选按钮的value***

```vue
<div id="app">
	<input type="radio" value="男" v-model="sex">
     <input type="radio" value="女" v-model="sex">
     <button @click="handleClick">点击收集数据</button>
</div>
<script>
	let vm =  new Vue({
        el:'#app',
        data:{
           sex:'男'， //收集单选按钮的value
        },
        methods:{
            handleClick(){
                // `${}` 是E6版本的模板字符串
                console.log(`单选框的数据是${this.sex}`)
            }
        }
  
    })
</script>
```

**3.单个复选按钮          收集的是一个布尔值  如果复选框选中 则收集的是true 反之false**

```vue
<div id="app">
	<input type="checkbox" v-model="checked">
    <buuton @click="handleClick">点击收集数据</buuton>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            checked:'', //收集的是布尔值
        },
        methods:{
            handleClick(){
                console.log(`单个复选框的按钮${this.checked}`)
            }
        }
        
    })
</script>
```

**4.多个复选按钮          收集的是一个数组   如果复选框选中 则收集的是value值 反之false**

```vue
<div id="app">
	<input type="checkbox" value="Jack" v-model="checkedNames">
    <input type="checkbox" value="John" v-model="checkedNames">
    <input type="checkbox" value="Mike" v-model="checkedNames">
     <button @click="handleClick">点击收集数据</button>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            checkedNames:[],
        },
        methods:{
            handleClick(){
                console.log(`多个复选按钮${this.checkedNames}`)
            }
        }
        
    })
</script>
```

**5.下拉框	收集的是option的value**

```vue
<div id="app">
	<select v-model="selected" multiple>
        <option>上海</option>
        <option>北京</option>
        <option>长沙</option>
    </select>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            selected:[], //收集下框的数据
        },
        methods:{
            handleClick(){
                console.log(`下拉框的数据是${this.selected}`)
            }
        }
        
    })
</script>
```

**相关修饰符**

| .number   | 处理数字格式的字符串  比如："123456" 变成数字可计算的 123456 |
| --------- | ------------------------------------------------------------ |
| **.lazy** | **延迟收集数据**                                             |
| **.trim** | **处理输入框数据的左右两侧空格**                             |

## 循环列表

**v-for 可以循环vue的数据   根据数据生成对应的标签结构**

```vue
<div>
   <ul>
       <li v-for="(item,index) of arr" v-bind:key="item">
       	{{index}}--{{item}}--<input type="text">
       </li>
    </ul>
    <button @click="handleclick">点击</button>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            arr:['我是云空','齐云空','张三','李四'],
            number:5,
            str:'heaven',
            person:{
                name:'yunkong',
                age:29,
                sex:'男'
            }
        }，
        methods:{
        	handleclick(){
        		//让arr随机排序
        		this.arr.sort(()=>Math.random()-0.5)
    		}
    	}
    })
</script>
```

 v-for 可以循环vue的数据 根据数据生成对应标签结构

| 数据是数组   | 得到两个变量 | item               | index |
| ------------ | ------------ | ------------------ | ----- |
| 数据是数字   | 得到两个变量 | item               | index |
| 数据是字符串 | 得到两个变量 | item               | index |
| s数据是对象  | 得到三个变量 | 属性值 属性名 索引 |       |

## 计算属性

```vue
<div id="app">
    
	<p>{methodsSum()}</p>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            number1:1,
            number2:2,
            number3:3,
            number4:4,
            number5:5,
        },
        methods:{
            methodsSum(){
                console.log('methodsSum')
                return this.number1 + this.number2 + this.number3 + this.number4
            }
        },
        computed:{
            computedSum:{ //计算后的属性 可以自定义
                get(){
                    //当依赖的属性改变时触发get函数
                    console.log('computedSum')
                    
                    //函数的return是计算属性显示在页面的值
                }
            }
        }
    })

</script>
```

## 绑定属性（指令）

 ***v-bind指令可以把标签的属性和vue的数据绑定在一块***

```vue
<div id="app">
    <h3 v-bind:yunkong="a">
       	我是标题
    </h3>
    <h3 :yunkong="a">
        我是标题
    </h3>
<div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            a:21342,
        }
    })    
</script>
```

> ​	1.v-bind:属性  可以简写成   :属性
> ​	2.vue可以把标签的样式 和对象/数组绑定在一块

**1.style和对象绑定在一块**

```vue
<div id="app">
    <div :style=styleObj>{{text}}</div>
<div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            styleObj:{
                backgroundColor:"lightblue",
                color:"pink"
            }
        }
    })    
</script>
```

**2.style和数字绑定在一块**

```vue
<div id="app">
    <div :style=styleArr>{{text}}</div>
<div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            text:'我是内容',
            styleArr:[
                {
             	 	backgroundColor:"lightblue",
                	color:"pink"
            	},
                {
                    color:"grey"
                }
            ]
        }
    })    
</script>
```

**3.class和字符串绑定在一块**

```vue
<div id="app">
	<div :class="'heaven'"> {{text}} </div>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            text:'我是内容'
        }
    })
</script>
```

**4.class和数组绑定在一块 把数组成员作为标签的类名**

```vue
<div id="app">
	<div :class="classArr">
         {{text}}
    </div>   
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            text:'云空'，
            classArr:['yunkong','version'],
        }
    })
</script>
```

**5.calss和对象绑定在一块 如果对象的属性值为true 则属性名会作为标签的类名**

```vue
<div id="#app">
    <div :class="classObj">
        {{text}}
    </div>
</div>
<script>
	let vm = new Vue({
        el:"#app",
        data:{
            text:'云空'，
            classArr:{
            	show:true,
            	isActive:true
        	}
        }
    })
</script>
```

## 控制属性（指令）

**1.v-if 控制单个dom元素显示**

```vue
<div id="app">
    <h3 v-if="number===1">我是标题</h3>
    <div v-else-if="number===2">我是div1</div>
    <div v-else-if="number===3">我是div2</div>
    <div v-else>我是div3</div>
</div>
<script>
	let vm = new Vue({
        data:{
            number:2,
        }
        
    })
</script>
```

**2.v-if 控制多个dom元素显示**

```vue
<template v-if="isShow">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</template>
<template v-if="loginType === 'username'">
    <label>用户名</label>
    <input placeholder="请输入用户名" key="1">
</template>
<template v-else >
    <label>密码</label>
    <input placeholder="请输入密码" key="2">
</template>
<script>
	let vm = new Vue({
        el:'#app',
        datea:{
            isShow:true,
            loginType:'password'
        },
        methods:{
            handleClick(){
                if(this.loginType === 'username'){
                    this.loginType = 'password'
                }else{
                    this.loginType = 'username'
                }
            }
        }
    })
</script>  
```

>  控制单个dom元素是否渲染(不是通过css)在页面上  如果是true 则渲染在页面上 反之不渲染
>    如果需要控制多个dom元素的显示 只要在template标签上使用v-if指令即可

**3.v-if 与 v-for 权限问题**

```vue
<div id="app">
    <ul>
        <li v-for="(todo,index) in todos" v-if="todo.isComplete">
            {{ index }}
        </li>
    </ul>
    <ul>
        <li v-for="(todo,index) in filterTodos">
            {{ index }}
        </li>
    </ul>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            todos:[
            	{isComplete:true},
                {isComplete:false},
                {isComplete:true}
        	]
        },
        computed:{
            // filterTodos:{   //把todos中isComplete值是false 都过滤掉
            //     get(){
            //         return this.todos.filter(item=>item.isComplete)
            //     }
            // }
            filterTodos(){
                return this.todos.filter(item=>item.isComplete)
            }
        }
    })
</script>
```

> **v-for 的优先级比 v-if 更高**
> **循环了三圈 却只生成了两个li**
> **不推荐在同一元素上使用 v-if 和 v-for**

## 显示属性（指令）

```vue
<div id="app">
    <h3 v-show="isShow">我是标题</h3>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
           	isShow:false,
        }
    })
</script>
```

**v-show**
    **控制单个dom元素是否显示（通过css）在页面上  如果是true 则显示在页面上 反之不显示**

**v-if  和  v-show**
	**当需要频繁的切换dom元素的显示时使用v-show  节省频繁创建dom 销毁dom元素的开销**

## 监听器（属性）

```vue
<div id="app">
    {{arr}}
    <button @click="handleClick">点击更新对象</button>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            number:1,
            arr:[0,1,2],
            person:{
                name:'yunkong',
                age:29
            },
            arr1:[{
                name:'yunkong',
                age:28
            },{
                name:'海文',
                age:29
            }]
        },
        methods:{
            handleClick(){
                this.number++
                // this.arr[0] = '云空'  //不能直接索引修改数组的数据
                 this.arr.push(1)
               	 console.log(this.arr)
                 this.person.name = '云空'
                 this.person.age = 30
                this.arr1[0].name = '白羊座的梦'
            }
        },
        //放置监听器
        watch:{
            number:{
                handler(){
                    console.log('number 数据变化 我监听到了')
                }，
            }
            arr:{
            	handler(){
        			console.log('arr数据变化了 我监听到了')
    			}，
        	}，
            "person.name":{//安装person的监听器 该监听器 可以监控对象内部认一个属性的变化
                handler(){//当person 变化时触发
                    console.log('person数据变化了 我监听到了')
                },
                deep:true, //控制到对象属性的改变
            }，
            arr1:{
                handler(){
                    console.log('arr1数据变化 我监控到了')
                }
                deep:true,
            }
        }
    })
</script>
```

> 通过使用数组的变异方法 watch是可以监控到的
> 修改数组的索引 改变数组 watch是不可以监控到的
> 通过修改对象person的属性  watch是可以监控到的
> 这样的监视器 默认是可以监控对象person内部任一个属性的变化
> 如果只需要监视对象person的某一个属性(例如name)的变化 则写成"person.name"

## 自定义指令(属性)

```vue
<div id="app">
    <p>{{message}}</p>
    <p v-text='message'></p>
    <p v-html='msg'></p>
    <p v-color="'pink'">我是自定义指令</p>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            message:'我是一波文本'，
            msg：'<a>我是a标签</a>'
        }，
        //局部指令 direactives 存放所有的自定义指令 
       	direactives:{
        	color:{ //定义指令的名字
        		bind(el,binging){ //修改dom元素的style
        			console.log(arguments)
        			el.style
    			},
                 inserted(el,binging){ //执行js方法
                     console.log('inserted执行')
                 },
                 update(){
                     console.log('update执行')
                 },
                 componentUpdated(){
                     console.log('componentUpdated执行')
                 }
    		},
             focus:{
                 bind(el,binging){
                     //console.log(arguments)
                     console.log('bind执行')
                     //console.log(el.focus)
                     //el.focus()
                     //
                 },
                 inserted(el,binging){
                     el.focus() //让元素获取焦点
                 }
             }
    	}
    })
</script>
```

## 过滤器

```vue
<div id="app">
	<p>价格：{{a|heaven|fn(2,3)}}</p>
    <p>{{sum}}</p>
    <p :heaven="a|haha">{{a|haha}}</p>
</div>
<script>
	let vm = new Vue({
        el:'#app',
        data:{
            a:12,
            number1:10,
            number2:20,
        },
        //局部过滤器 放置所有的过滤器函数
        filters:{
            heaven(data){
                console.log(data,'heaven过滤器函数 接收到了管道左侧的数据')
                return '$'+data //返回结构 $12
            },
            fn(data,a,b){
                console.log(arguments,'fn过滤器函数 接收到了管道符左侧的数据')
                return data + a + b //返回结果 $1223
            }
            comput
        }
    })
</script>
```

## 生命周期函数

**生命周期函数就是在vue组件在某个时间段会自动执行的函数**

 

| 生命周期函数  | 数据                                                         | 触发周期                | 作用                                  |
| ------------- | ------------------------------------------------------------ | ----------------------- | ------------------------------------- |
| beforeCreate  | 没有初始任何数据 有属性 但是没有属性值，值位undefined        | 开始                    |                                       |
| created       | 初始化基础数据 data methods computed watch 这些都有值        | 数据初始化              | 在该函数中发送ajax请求 获取初始的数据 |
| beforeMount   | 该状态中的数据和created一致  自己 ：指令的                   | 初始化完成              |                                       |
| mounted       | 把created准备好的数据 注入到页面中                           | 数据挂载到dom上（页面） |                                       |
| beforeUpdate  | 当页面重新渲染前触发<br /> 如果只改变组件的数据 却没有导致重新渲染 则不会触发该函数 |                         |                                       |
| updated       | 当页面重新渲染之后触发                                       |                         |                                       |
| beforeDestroy | 在组件销毁之前触发                                           | 组件摧毁之前            | 在该函数中 销毁组件内部的定时器       |
| destroyed     | 在该函数中销毁组件内部的定时器 在组件销毁之后触发            | 组件摧毁之后            |                                       |

```javascript
let vm = new Vue(){
	el:'#app',
	data:{
		a:12,
},
beforeCreate(){
     console.log(1111,'beforeCreate')
     // debugger
 },
 created(){
     console.log(2222,'created')
     // debugger
 },
 beforeMount(){
     console.log(3333,'beforeMount')
     // debugger
},
mounted(){
    console.log(4444,'mounted')
    // debugger
},
beforeUpdate(){
    console.log(5555,'beforeUpdate')
},
updated(){
    console.log(6666,'updated')
},
beforeDestroy(){
    console.log(7777,'beforeDestroy')
},
 destroyed(){
     console.log(8888,'destroyed')
 }


}
```

## VUE组件

组件是html+css+js结合出的标签

 局部组件

```vue
<div id="app">
    {{a}}
    <yunkong>
    
    </yunkong>
</div>
<script>
	let yunkong = Vue.extend({
        template:`<div>
    		<p>我是子组件的p标签</p>
			<button>我是子组件的按钮标签</button>
    	</div>`
    })
    //template(模板)    是配置html代码
    
    
    let vm = new Vue({
        el:'#app',
        data:{
            a:1,
        },
        //放置根组件
        components:{
            yunkong
        }
        
    })
</script>
```

1. 生出组件 Vue.extend （局部组件）
2. 注册组件 components(在根组件的属性)
3. 使用组件  在根组件中使用

模板组件

```html
<template></template> <!--模板标签-->
```

```vue
<div id="app">
    {{a}}
    <template id="fn">
    	<div>
    		<p>我是子组件的p标签</p>
			<button>我是子组件的按钮标签</button>
    	</div>
    </template>
</div>
<script>
	let yunkong = Vue.extend({
        template:'#fn'
    })
    let vm = new Vue({
        el:'#app',
        data:{
            a:1,
        },
        //放置根组件
        components:{
            yunkong
        }
        
    })
</script>
```

解析组件

```html
<script type="text/x-template" id="yunkong">
	<div>我是子组件 </div>
</script>
```

全局组件

```html
<template id="#common">
	<div>
        我是全局组件
    </div>
</template>
<script>
 	//定义全局组件
	Vue.component('common',{
        template:'#common',
    })
</script>
```

1. 生成组件 Vue.component (全局组件)
2. 使用组件

## 子组件的data选项

在子组件中data必须是函数形式

```vue

<div id="app">
    <heaven></heaven>
    <heaven></heaven>
    <heaven></heaven>
</div>

<!--定义heaven组件的模板-->
<template id="heaven">
    <div>
        <span>{{number}}</span>
        <button @click="handleClick">按钮</button>
    </div>
</template>

<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>
<script>


    /*
    *   子组件中data选项必须是个函数
    *   而且返回一个对象
    *   在该对象中定义组件的数据
    * */
    let heaven = {
        template:'#heaven',
        // data:{      //每次使用heaven组件data的数据都是用一个对象
        //     number:10
        // },
        methods:{
            handleClick(){
                this.number++
            }
        },
        data:function(){  //每次使用heaven组件data的数据都是函数执行后返回的不同对象 简写data:(){}
            return {
                number:10
            }
        },
        //是钩子函数created是在组件生出时触发
        created(){
            console.log('子组件created')
        }
    }
    
    let vm = new Vue({  //根组件
        el:'#app',
        data:{
            a:'我是根组件'
        },
        //放置根组件的所有子组件
        components:{
            heaven
        }

    })
</script>

```

## 组件的通讯

```vue
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    {{person}}
    <heaven
            :msg="msg"
            :arr="arr"
            :person="person"
            v-bind="person"
    ></heaven>
</div>

<!--定义heaven组件的模板-->
<template id="heaven">
    <div>
        我是子组件
        <button @click="handleClick">按钮</button>
    </div>
</template>


<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>
<script>

    /*
    *   父组件如何把数据传递给子组件
    *       通过绑定属性即可
    *       $props  存放子组件接受的父组件数据
    *       $attrs  存放子组件没有接受的父组件数据 v-bind="person"
    *       $destroy    销毁组件
    *       $set        设置对象的某个属性是响应式的
    * */

    let heaven = {
        template:'#heaven',
        props:['msg','name','age'],
        data(){
            return {
                //把父组件的数据 赋值给 子组件的数据 才可以进行
                myAge:this.$props.age
            }
        },
        //生命周期函数;
        created(){
            // console.log(this.$props.msg)
            // console.log(this.$attrs)
        },
        methods:{
            handleClick(){
                // console.log(this.$props.age)
                // this.$props.age++
                // this.myAge++
            }
        }

    }

    let vm = new Vue({  //根组件
        el:'#app',
        data:{
            msg:'我是根组件的数据',
            arr:[1,2,3],
            person:{
                name:'heaven',
                age:29
            }

        },
        //放置根组件的所有子组件
        components:{
            heaven
        }
    })
</script>
</body>
</html>
```



props数据检测

```vue
<div id="app">
    <!--:msg="msg"传递数据 -->
    <heaven :msg="msg"></heaven>
</div>
<template id="yunkong">
	<div>
        {{msg}}
    </div>
</template>
<script>
    //子组件
	let yunkong = {
        template:'#yunkong', //模板
        //prpos:['msg']
        props:{
            msg:{ //接受msg属性的
               type:String, //数据类型检查
               required:true //是否必须传递    
            },
            a:{
            	default:100, //当父组件没有传递该属性 则默认值生效
        	},
            b:{
                validateor(value){ //自定义校验规则 返回true则验证通过 反之验证不通过
                    if(value > 300){
                        return true;
                    }
                   //console.log(arguments)
                }
            }    
        }     
    }
    //父组件
    let vm = new Vue({
        el:'#app',
        data:{
            msg:'我是根组件'
        },
        //放置根组件的所有子组件
        components:{
            yunkong
        }
    })
</script>
```

子组件向父组件传数据

```vue
<div id="app">
    <!--:msg="msg"传递数据 -->
    <heaven :number="number" v-on:xxx="handleXXX"></heaven>
</div>
<template id="yunkong">
	<div>
        {{msg}}
        我是子组件
        <button @click="handleClick">按钮</button>
    </div>
</template>
<script>
	let yunkong = { //子组件
        template:'#yunkong',
        props:['msg'],
        methods:{
            //点击按钮处理函数
            handleClick(){
               // 子组件让父组件修改自己的number数据
               this.$emit('xxx',this.msg) //触发一个事件
            }
        }
    }
	let vm = new Vue({ //根组件 
        el:'#app',
        data:{
            number:20,
        },
        //放置所有的子组件
        components:{
            yunkong
        },
        methods:{
            handleXXX(){
                console.log('xxx事件被触发了 我监控到了')
            }
        }
           
    })
</script>
```

非父子组件（兄弟）传值

```vue
<div id="app">
   <son1></son1>
    <son2></son2>
</div>

<!---定义heaven 组件的模板-->
<template id="son1">
	<div>
        我是son1组件
        <button @click="handleClick">点击发送son1组件的数据</button>
    </div>
</template>
<template id="son2">
	<div>
        我是son2组件
    </div>
</template>

<!--Vue代码-->
<script>
    //事件车 兄弟组件提供这个eventBus对象进行事件传递
    let eventBus = new Vue();
    let son1 = {
        template:'#son1',
        data(){
            return{
                msg:'我是son1组件的数据'
            }
        }
        methods:{
        	handleClick(){
                //把组件的msg发送给son2组件
                eventBus.$emit('xxx',this.msg)
                //son2 组件如何监听到son1组件发射了 xxx事件了
                //son2 组件如何绑定xxx 事件？？
                
            }
    	}
    }
    let son2 = {
        template:'#son2',
        created(){
            eventBus.$on('xxx',function(msg){
                console.log('son1 组件发射了xxx事件 我监控到了',msg)
            })
        }
    }
    let vm = new Vue({ //根组件 
        el:'#app',
        data:{
            number:20,
        },
        //放置所有的子组件
        components:{
           son1,
           son2
        },
        methods:{
            handleXXX(){
                console.log('xxx事件被触发了 我监控到了')
            }
        }
           
    })
</script>
```

组件之间的访问

```vue
<div id="app">
    <son1></son1>
    <son2></son2>
    <button @click="getChildren">
      点击 获取子组件的数据
    </button>
</div>

<!---定义heaven 组件的模板-->
<template id="son1">
	<div>
        我是son1组件
        <button @click="getParent">点击 获取父组件的数据</button>
    </div>
</template>
<template id="son2">
	<div>
        我是son2组件
    </div>
</template>


<!--Vue代码-->
<script>
    //事件车 兄弟组件提供这个eventBus对象进行事件传递
    let eventBus = new Vue();
    let son1 = {
        template:'#son1',
        methods:{
            getParent(){ //son1 组件要获取父组件的数据
                console.log('父组件的数据主动',this.$parent.number)
                //根组件的数据
                console.log(this.$root.number)
                this.$parent.number++;
            }
        }
    }
    let son2 = {
        template:'#son2',
      
    }
    let vm = new Vue({ //根组件 
        el:'#app',
          data:{
            number:20,
        },
        //放置所有的子组件
        components:{
           son1,
           son2
        },
        methods:{
            getChildren(){
                //$children 是子组件的集合
                console.log(this);
            }
        }
           
    })
</script>


```

vue8