# React

## React 的简介

 React官网：<https://react.docschina.org/>

 bootcdn在线引入前端的代码库：<https://www.bootcdn.cn/>

```html
<!--react 代码引入 development代表开发版本-->
<script src="https://cdn.bootcss.com/react/16.10.2/umd/react.development.js"></script>
<!--react-dom 代码引入 min代表已经压缩  -->
<script src="https://cdn.bootcss.com/react-dom/16.10.2/umd/react-dom.development.js"></script>
```

## React 代码的使用

```html

<html>
    <head>
        <meta charset="UTF-8">
        <title>React</title>
    </head>
    <body>
		<!--react 代码引入 development代表开发版本-->
		<script src="https://cdn.bootcss.com/react/16.10.2/umd/react.development.js"></script>
		<!--react-dom 代码引入 min代表已经压缩  -->
		<script src="https://cdn.bootcss.com/react-dom/16.10.2/umd/react-dom.development.js">	</script>
     <div id="app"></div>
	<script>
        let vDom = React.ceateElement('p',{},'我是p标签')
        let vDom1 = React.createElement('h2',{
            id:'yunkong'
        },vDom)
        
        //把虚拟dom挂载到真实dom上
        ReactDOM.render(vDom1,document.getElementById('app'));
	</script>        
    </body>
</html>
```

1. 如何创建虚拟dom React.cretaElement(节点的类型,节点的属性,节点的内容)
2. 虚拟dom和真实dom的区别
   1. 虚拟dom是一个对象 只有10多个属性
   2. 真实dom是一个对象 有很多个属性

网页的断点

```html
debugger
```

## React 开始jsx编写

引入babel.js  

```html
<script src="https://cdn.bootcss.com/babel-standalone/7.0.0-beta.3/babel.js"></script>
<!--一定要修改type="text/babel"-->
<script type="text/babel"></script> 
```

作用：可以html+js的写法（可以理解为混合双打）

语法：jsx

代码演示

```jsx
//创建虚拟dom 然后把虚拟dom挂载到 真实dom上      
let vDom = <h2 id="heaven" title="我是yunkong"><p>我是p标签</p></h2>; 
ReactDOM.render(vDom1,document.getElementById('app'));
```

可以带有参数

```jsx
let a = '齐云飞'，
 	b = 'yunkong'，
   	c = '文本内容'；
//创建虚拟dom jsx ---》 JavaScript + xml
let vDom = (
    <h2 id={a} tiltle={b}>{c}</h2>
)
ReactDOM.render(vDom1,document.getElementById('app'));
```

#### 添加事件(必须是on+事件名 并且事件需要大写)

```jsx
let a = '齐云飞'，
 	b = 'yunkong'，
   	c = '文本内容'；
//创建虚拟dom jsx ---》 JavaScript + xml
function fn(){
    console.log('执行')
}
let vDom = (
    <h2 id={a} onClick={fn} tiltle={b}>{c}</h2>
)
ReactDOM.render(vDom1,document.getElementById('app'));
```

#### 列表显示(map 函数)

```jsx
let arr = ['html','css','javascript','node','react']
//map 循环遍历 参数回调函数
let vDom = (<ul>{arr.map((item)=>{return <li>{item}</li>})}</ul>)
ReactDOM.render(vDom,document.getElementById('app'))
```

添加key值

```jsx
let arr = ['html','css','javascript','node','react']
//map 循环遍历 参数回调函数 当只有一句话是 可以不写 return
let vDom = (<ul>{arr.map((item)=><li key={item}>{item}</li>)}</ul>)
ReactDOM.render(vDom,document.getElementById('app'))
```

#### 列表显示（reduce 函数）

```jsx
let vDom2 = (
	<ul>
    	{
            arr.reduce((pre,next)=>{
                pre.push(<li key={next}>{next}</li>)
            	return pre
            },[])
        }	
    </ul>
)
ReactDOM.render(vDom2,document.getElementById('app'))
```

添加css属性

```jsx
let vDom3 = <h2 style={{backgroundColor:'pink'}}>我是h2标签</h2>
ReactDOM.render(vDom3,document.getElementById('app'))
```

style={js对象}， style={{对象的属性名：属性值}}；

```jsx
//单位是默认好了 px
let styleObj = {backgroundColor:'pink',fontSize:30};
let vDom3 = <h2 style={styleObj}>我是h2标签</h2>
```



## React 函数组件

1. ​	每个网页都是多个功能模块组成的
2. ​    每个模块都有自己的css html js
3. ​    功能模块就是react中的组件

#### 定义函数组件

```jsx
//定义一个函数组件
function Person(){
	return <h2>我是函数组件</h2>
}

//把组件挂载到页面中 <Person></Person> <Person/>
ReactDOM.render(<Person></Person>,document.getElementById('app'))
```

​	ReactDOM.render 函数 可以渲染虚拟dom 也可以渲染组件

```jsx
//定义一个函数组件
function Person(props){
    console.log(props);
	return <h2>我是函数组件</h2>;
}

//把组件挂载到页面中 <Person></Person>   简写：<Person/>
ReactDOM.render(<Person id="a" name="b"/>,document.getElementById('app'))
```

​		标签名必须大写

​		渲染组件时 组件的属性名组成的对象作为实参传递到函数组件中（props）

#### 检测数据类型

​	引入一个包，才可以使用

```html
<!--检查prop-types的包-->
<script src="https://unpkg.com/prop-types@15.6/prop-types.js"></script>
```

```jsx
//定义一个函数组件
function Person(props){
    console.log(props);
	return <h2>我是函数组件</h2>;
}

let a = 2,
    b = 'yunkong';

//指定Person组件接受的数据类型
Person.propTypes ={
 	//id:PropTypes.number, 	//接受的id的数据类型必须是number
	name:PropTypes.string.isRequired, //isRequired 这个属性必须传递
}

//把组件挂载到页面中 <Person></Person>   简写：<Person/>
ReactDOM.render(<Person id={a} name={b}/>,document.getElementById('app'))
```

#### 设置默认的属性

```jsx
//定义一个函数组件
function Person(props){
    console.log(props);
	return <h2>我是函数组件</h2>;
}

let a = 2,
    b = 'yunkong';

//设置Person组件的默认属性
Person.defaultProps = {
    name:'heaven',    //当外部已经传递name属性 就不会生效
    age:28
}

//把组件挂载到页面中 <Person></Person>   简写：<Person/>
ReactDOM.render(<Person id={a} name={b}/>,document.getElementById('app'))
```

## React 类组件

#### 定义类组件

```jsx
//es6的类组件 这个组件继承了React.Component 这个组件的特效
class Person extends React.Component{
   	constructor(props){ //继承父类constructor 函数中的属性
        super();
        console.log(props);
    }
    
    render(){
        console.log(this.props);
        return <h2>我是es6类组件(复杂组件)</h2>
    }
}
Person.propTypes = {
    name:PropTypes.string.isRequired,
}

ReactDOM.render(<Person name="yunkong" a="云空"></Person>,document.getElementById('app'))
```

#### 对象传值

```jsx
//es6的类组件 这个组件继承了React.Component 这个组件的特效
class Person extends React.Component{
   	constructor(props){ //继承父类constructor 函数中的属性
        super();
        console.log(props);
    }
    
    render(){
        console.log(this.props);
        return <h2>我是es6类组件(复杂组件)</h2>
    }
}
Person.propTypes = {
    name:PropTypes.string.isRequired,
}
let obj = {
    name:'heaven',
    age:28,
    sex:'男'
    
}
//{...obj} 使用了配置运算符
ReactDOM.render(<Person {...obj}></Person>,document.getElementById('app'))
```

#### state 初始化

```jsx
class App extends React.Component{
 	constructor(props){
		super(props);
		this.state = { //定义初始的状态
			count:0
		}
    }  
    render(){
        const {count} = this.state //结构赋值
        console.log(this.state)
        return <div>我是es6的类组件（复杂组件）{conunt}</div>
    }   
}
ReactDOM.render(<App/>,document.getElementById('app'))
```

​		props 是外部传递给组件的，在组件内部不可以修改props,函数组件和es6类组件都有props

​		state 定义组件时自动创建的，es6类组件才有state，函数组件内部没有			

#### state 对象的属性值进行变化

```jsx
class App extends React.Component{
 	constructor(props){
		super(props);
		this.state = { //定义初始的状态
			count:0
		}
    }
    hanleClick(){
        conole.log(this) //在没有用（bind函数）修改this指向时 默认是Window 对象
        console.log('执行')；
       // ++this.state.count； //state.count 加一
        //console.log(this.state.count); //打印变化的值
        let {count} = this.state;	//取出state中的count的值
        count++;	//进行加一
        this.setState({	//修改count值
            count:count	//传递对象 可以简写成 count
        })
    }
    render(){ //当state 的数据发生变化时 就会自动触发
        const {count} = this.state //结构赋值
        console.log(this.state);
        console.log(this) //this是实例化对象 App类 实例出来的
        //this.hanleClick.bind(this) bind()函数的作用是修改this指向 （修改成指向实例化对象）
        return <div onClick={this.hanleClick.bind(this)}>我是es6的类组件（复杂组件）{conunt}</div>
    }   
}
ReactDOM.render(<App/>,document.getElementById('app'))
```

​		重点：必须通过setState这个函数改变了state的数据 才会自动触发 render的函数

​		注意：函数组件是没有state这个属性的，而类组件默认就有个state属性，但是属性值是null

#### setState方法

| 名称                              | 作用                | 用法                |
| --------------------------------- | ------------------- | ------------------- |
| this.setState(state=>({对象:值 }) | 改变state里的属性值 | 上一次和state有关系 |
| this.setState({对象:值})          | 改变state里的属性值 | 上一次和state没关系 |



#### 空白节点

```jsx
const Fragment = React.Fragment; //空的按位组件
```

作用是用于嵌套的标签的父亲作用。

#### 案例练习（显示隐藏效果）

```jsx

<div id=“app”></div>

<script type="text/babel">
const Fragment = React.Fragment;
class App extends React.Component{
	constructor(){
		super()
		this.state = {
			isShow:false //记录显示隐藏 默认flase 表示是隐藏的
		}
	}
	onBtn(){
		let {isShow} = this.state;
		isShow=!isShow;
		this.setState({
			isShow,
		})
		console.log(isShow);
	}
	render(){
		const {isShow} = this.state; //拿到flase
		return(
		<Fragment>
			<button onClick={this.onBtn.bind(this)} >点击切换</button>
			<div style={{display:isShow?'block':'none'}}>我是一个div标签</div>	
		</Fragment>
		)
	}
}
ReactDOM.render(<App/>,document.getElementById('app'))
 </script>
```

## React 非受控表单

ref获取原生dom

```jsx
class App extends React.Component{
    constructor(){
        super()
        this.sex=React.createRef() //最新的ref标记语法
        console.log(this.sex) //默认有current的对象（用来存储原生dom对象） 初始值位null
    }
    handleSubmit(e){  // e 表示事件对象
        e.preventDefault(); //阻止提交的默认刷新页面的行为
        //通过refs 获取表单元素（标签） 打印标记集合
        console.log(this.refs)
        //获取ref是字符串形式的
        console.log(this.refs.username.value); //打印被标记的username的value值
        //获取ref是箭头函数形式的
        console.log(this.yun);  //打印是（密码）input对象（dom）
        //获取ref是对象形式的
        console.log(this.sex) 
        console.log(this.sex.current) //打印是（性别）input对象（dom）
    }
    render(){
        return(
            // action 请求的url method请求方式 ref表示标记
        	<form action="/heaven" method="get"> 
            	用户：<input type="text" ref="username" /> <br/>  
                密码：<input type="password" ref={(psd)=>{this.yun=psd}} /> <br/>
                性别：<input type="text" /> <br/>
                <input type="submit" onClick={this.handleSubmit.bind(this)} />
            </form>
        )
    }
}
```

## React受控表单

```jsx
class App extends React.Component{
    constructor(){
		super()
		this.state = { //state记录的是一种状态 
             //收集用户输入的数据 value={username} 把input的value值和state的username邦定一起
			username:'',
            //收集用户输入的密码
			password:'', 
		}
        //提前修改this指向
        //this.handleUserChange = this.handleUserChange.bind(this)
    }
    //在input中输入数据的时候 就会触发的事件处理函数
    handleUserChange(e){
       console.log(this);
       console.log(e.target.value)
       this.setState({
           username:e.target.value
       })
    }
     handlePasChange(e){
       console.log(this);
       console.log(e.target.value)
       this.setState({
           password:e.target.value
       })
    }
    render(){
      //获取定义的值
      const{username,password} = this.state
       return (
       		 // action 请求的url method请求方式 ref表示标记
        	<form action="/heaven" method="get"> 
         		用户：<input type="text" value={username} onChange={this.handleUserChange.bind(this)} /> <br/>  
                密码：<input type="password"  value={password} onChange={this.handlePasChange.bind(this)} /> <br/>
                <input type="submit"  />
            </form>
       )
   }
}
```

## React todolist 案例

####  todolist 普通函数

```jsx
class App extends React.Component{
    constructor(props){
        super(props)
        this.state = {
          list:['吃饭','看书','看电影'], //存储当前已经做的事情
		  inputValue:'', //存储input的数据
        }
        //提前修改函数this指向
        //给this （实例化对象） 上设置了handleChang属性 值是一个内部this指向实例化对象的函数
	    this.hendleChange = this.hendleChange.bind(this);
	    this.handleAdd = this.handleAdd.bind(this);
		//this.handleDelete = this.handleDelete.bind(this);
    }
    
    hendleChange(e){
		//console.log(this);	打印是否 实例化的对象
		//使用setState() 函数修改数据 (状态）
		this.setState ({
			inputValue:e.target.value,
		})
	}
	handleAdd(){
		//console.log(this) 打印是否 实例化的对象
		//获取inputValue 
		let {inputValue,list} = this.state
		//修改state中的list数据
		//push() 方法可向数组的末尾添加一个或多个元素，并返回新的长度
		//unshift() 方法可向数组的开始添加一个或多个元素，并返回新的长度
		list.push(inputValue) 
		this.setState({
			//list:[...list,inputValue], //...list 把list数组进行展开，在和inputValue进行合并
			inputValue:'',
			list:list,
		})
	}
	handleDelete(index){ //index 接受bind函数传过来的index
		const {list} = this.state;
		//splice(数组索引,删除的个数) 方法 用于添加或删除数组中的元素。 返回的新数组
		list.splice(index,1)
		this.setState({
			list
		})
	}
	render(){
        const {list} = this.state;
		return(
        	<div>
                <input type="text"  value={inputValue} onChange={this.hendleChange}/>
                <button onClick={this.handleAdd}>add#{list.length}</button>
		    </div>
             <ul>
                 {
  list.map((item,index)=><li key={item} onClick={this.handleDetete.bind(this,index)}>{item}</li>)
                 }
             </ul>
        )
	}
}
ReactDOM.render(<App/>,document.getElementById('app'))
```

#### 	todolist 箭头函数

```jsx
class App extends React.Component{
    constructor(props){
        super(props)
        this.state = {
          list:['吃饭','看书','看电影'], //存储当前已经做的事情
		  inputValue:'', //存储input的数据
        }
    }
    
    hendleChange=(e)=>{
		//console.log(this);	打印是否 实例化的对象
		//使用setState() 函数修改数据 (状态）
		this.setState ({
			inputValue:e.target.value,
		})
	}
	handleAdd=()=>{
		//console.log(this) 打印是否 实例化的对象
		//获取inputValue 
		let {inputValue,list} = this.state
		//修改state中的list数据
		//push() 方法可向数组的末尾添加一个或多个元素，并返回新的长度
		//unshift() 方法可向数组的开始添加一个或多个元素，并返回新的长度
		list.push(inputValue) 
		this.setState({
			//list:[...list,inputValue], //...list 把list数组进行展开，在和inputValue进行合并
			inputValue:'',
			list:list,
		})
	}
	handleDelete=(index)=>{ //index 接受bind函数传过来的index
		const {list} = this.state;
		//splice(数组索引,删除的个数) 方法 用于添加或删除数组中的元素。 返回的新数组
		list.splice(index,1)
		this.setState({
			list,
		})
	}
	render(){
        const {list} = this.state;
		return(
        	<div>
                <input type="text"  value={inputValue} onChange={this.hendleChange}/>
                <button onClick={this.handleAdd}>add#{list.length}</button>
		    </div>
             <ul>
                 {
 					list.map((item,index)=>{
						return (
                            	<li onClick={()=>{this.handleDetete.bind(index)}} key={item}>
                                	{item}
                            	</li>
                           )
					})
                 }
             </ul>
        )
	}
}
ReactDOM.render(<App/>,document.getElementById('app'))
```

#### todolist 父子组件

```jsx
const {Component,Fragment} = React;
class App extends Component{
     state = {
         list:['吃饭','看书','看电影'], //存储当前已经做的事情
         inputValue:'', //存储input的数据
     }
    handleAppChange = (inputValue)=>{
        console.log(inputValue);
        this.setState({
            inputValue,
        })
    }
    handleListAdd = ()=>{
		console.log(1);
        this.setState({
            list:[this.state.inputValue,...this.state.list],
            inputValue:'',
        })
    }
    handleAppDelete = (index)=>{
        console.log(index);
        const {list} = this.state;
        list.splice(index,1)
        this.setState({list})
    }
	render(){
        const {list,inputValue} = this.state;
		return(
        	 <Fragment>
                <Add inputValue={inputValue}
                     handleAppChange={this.handleAppChange}
                     list={list}
                     handleListAdd={this.handleListAdd}
                 />
                <List list={list} handleAppDelete={this.handleAppDelete}/>
             </Fragment>
        )
        // <List list={list }/> 传地参数 作为props的属性进行传递
	}
}
//添加组件(子组件)
class Add extends Component{
    hendleChange=(e)=>{
       //需要更改 父组件中的inputValue 通知父组件修改组件的inpuValue数据
       this.props.handleAppChange(e.target.value) //调用父类的方法  handleAppChange
	}
    handleAdd=()=>{
        //需要修改 父组件的list数据
        this.props.handleListAdd()
    }
    render(){
        const {inputValue,list} = this.props
        return(
            <Fragment>
                <input type="text"  value={inputValue} onChange={this.hendleChange}/>
                <button onClick={this.handleAdd}>add#{list.length}</button>
            </Fragment>
        )
    }
}

//列表组件(子组件)
class List extends Component{
    	
        handleItemDelete = (index) =>{
            console.log(index);
            this.props.handleAppDelete(index)
        }
        getListNodes =()=>{
            const {list} = this.props
            return list.reduce((pre,next,index)=>{
                   pre.push(
                        <li onClick={()=>this.handleItemDelete(index)} key={next}>{next}</li>
                    )
                   return pre
              },[])
    	
        }
        render(){
            console.log(this.props)
            return(
                <Fragment>
                   <ul>
                      {this. getListNodes()}
                   </ul>
                </Fragment>
            )
        }
}
ReactDOM.render(<App/>,document.getElementById('app'))
```

## React 生命周期函数（钩子函数）

#### mount阶段（挂载阶段）

```jsx
 UNSAF_componentWillMount(){} //当组件还没有挂载真实dom时 触发
 render(){} //当组件的state和props发生变化时
 componentDidMount(){} //当组件已经挂载到真实dom时
```

```jsx
class Life extends React.Component{
	state = {
		count:0,
	}
	handleClick = ()=>{
		const {count} = this.state
		count++;
		this.setState({
            count
        })
	}
    //当组件还没有挂载真实dom时 触发 只能执行一次
    //（老版本：componentWillMount）（新的版本：UNSAFE_componentWillMount）
    UNSAF_componentWillMount(){
       console.log('Life 组件componentWillMount');
    }
	
	//当组件的state和props发生变化时 触发 真个
	render(){
         console.log('render执行')
         let {count} = this.state
		return <div onClick={this.handleChlick}>我是div</div>
	
	}
	//当组件已经挂载到真实dom时 触发 在整个组件的生命周期中 只能执行一次
	componentDidMount(){
        console.log('Life 组件componentDidMount');
    }
}
ReactDOM.render(<Life/>,document.getElementById('app'))
```

#### update阶段

```jsx
shouldcomponentUpdate(){} //是否允许组件更新
UNASFE_componentWillUpdate(){} //当数据更新前触发
componentDidUpdate(){} //当数据更新后触发
```

```jsx
class Life extends React.Component{
	state = {
		count:0,
	}
	handleClick = ()=>{
		const {count} = this.state
		count++;
		this.setState({
            count
        })
	}
   //可以让组件的数据更新吗,(赋予组件是否更新的权力)(是否允许组件更新)
	//即使state和props数据变化了 也不能更新组件
	shouldComponentUpdate(){
		console.log('life 组件 shouldComponentUpadate');
		return false;
	}
    //当组件的state和变化前
   UNSAFE_componentWillUpdate(){
		console.log("当数据变化前 UNSAFE_componentWillUpdate触发")
	}
	
	//当组件的state和props发生变化时 触发 真个
	render(){
         console.log('render执行')
         let {count} = this.state
		return <div onClick={this.handleChlick}>我是div</div>
	
	}
	//当组件的state和props变化后
	componentDidUpdate(){
		console.log("当数据变化完成时 componentDidUpdate触发")
	}
	
}
ReactDOM.render(<Life/>,document.getElementById('app'))
```

#### props 周期函数

```jsx
UNSAFE_componentWillReceiveProps(){} //当组件接受的props改变了之后 就会自动触发 
```

```jsx
class App extends Component{
	state = {
		count:0,
	}

	handleChlick = ()=>{
		let {count} = this.state;
		count++;
		this.setState({
			count
		})
	}
	
	render(){
		console.log('render执行')
		let {count} = this.state
		return (
		<Fragment>
			<div onClick={this.handleChlick}>我是div{count}</div>
			<Son count={count} />
		</Fragment>
		)
	}
}
class Son extends Component{
	//当组件接受的props改变了之后 就会自动触发
    //nextProps是下次更新的数据
	UNSAFE_componentWillReceiveProps(){
		console.log('son 组件 UNSAFE_componentWillReceiveProps触发');
	}
	render(){
		console.log(this.props)
		return (
			<div>我是子组件</div>
		)
	}
}
```

#### 销毁周期

```jsx
componetWillUnmount(){}  //销毁组件
```

```jsx
class App extends Component{
	state = {
		count:0,
		list:['html','css','js','node']
	}

	handleChlick = ()=>{
		//销毁组件
		ReactDOM.unmountComponentAtNode(document.getElementById('app'))
	}
	handleLifeDelete = (index)=>{
		const {list} = this.state
		list.splice(index,1)
		this.setState({list})
	}
	render(){
		console.log('render执行')
		let {count,list} = this.state
		return (
		<ul>
			{list.map((item,index)=><Son key={item} handleLifeDlete={()=>this.handleLifeDelete(index)} item={item}/>)}
		</ul>
		)
	}
}
class Son extends Component{
	componentWillUnmount(){
		console.log('组件被卸载');
	}
	handleItemDelete = ()=>{
		this.props.handleLifeDlete()
	}
	render(){
		return (
			<li onClick={this.handleItemDelete}>{this.props.item}</li>
		)
	}
	componetWillUnMount(){
		conole.log("组件被销毁了")
	}
}
ReactDOM.render(<App/>,document.getElementById('app'))
```

## React 组件间的通信

#### 	子组件和父组件通信 

```jsx
//通过属性传递(props)
class Parent extends Component{
	state = {
		msg:'我是父组件的数据'
	}

	xxx = (msg)=>{	//设置参数接收子组件传来的数据
		console.log('传递来的数据:--->'+msg)
		console.log('我是父组件的函数')
	}

	render(){
		return(
			<div>
				<div>我是父组件</div>
				<hr/>
				<Son xxx={this.xxx} mag={this.state.msg}></Son>
			</div>
		)
	}
}
class Son extends Component{
	state = {
		msg:'我是子组件数据'
	}

	sendMsg = ()=>{ //这个函数内部 需要把子组件的msg数据 发送给parent组件
		this.props.xxx(this.state.msg); //触发父组件的传来的xxx函数 还可以把子组件的state数据传递过去
	}

	render(){
		console.log(this.props) //打印props对象
		return(
			<div>
				<div>我是子组件</div>
				<button onClick = {this.sendMsg }>点击发送子组件的msg数据</button>
			</div>
		)
	}
}
ReactDOM.render(<Parent/>,document.getElementById('app'))   
```

#### 	兄弟组件的通信

​	引入一个cdn pubsub.js

```jsx
<!-- 让两个哥们一起干 -->
<script src="https://cdn.bootcss.com/pubsub-js/1.7.0/pubsub.js"></script>
```

```jsx
//父组件
class Parent extends React.Component{
	render(){
		return(
			<div>
				<Son1/>
				<hr/>
				<Son2/>
			</div>
		)
	}	
}
//Son1 组件
class Son1 extends React.Component{
	state = {
		msg:'我是son1组件中数据'
	}

	//发送数据
	sendMsg = ()=>{ //这个函数要做的是 触发son2组件的yyy事件
		PubSub.publish('yyy',this.state.msg);
		console.log('我被点击了--我是Son1按钮')
	}
    
	//接受数据
	//使用钩子函数
	componentDidMount(){	//在这个函数中我们需要
		//订阅了yyy事件 刚开始yyy事件不会触发 一旦触发了yyy事件 就会执行第二个回调函数
		PubSub.subscribe('xxx',this.getMsg1);
	}

	getMsg1 = (type,date)=>{
		//type 订阅事件名 date 数据
		console.log('我在Son1中打印接受来的son2的数据--》 ',type,date)	 //arguments?
	}
	render(){
		return(
			<div>
				<button onClick={this.sendMsg}>点击发送数据给son2组件</button>
				<div>我是son1组件 数据---》：{this.state.msg}</div>
			</div>
		)
	}
}
//Son2 组件
class Son2 extends React.Component{ 
	state = {
		msg:'我是son2组件的数据'
	}

	//发送数据 state 
	sendMsg = ()=>{ //这个函数要做的是 触发son2组件的yyy事件
		PubSub.publish('xxx',this.state.msg);  //发送数据
		console.log('我被点击了--我是Son2按钮')
	}
    
	//接受数据 state
	getMsg2 = (type,date)=>{
		//type 订阅事件名 date 数据
		console.log('我在Son2中打印接受来的son1的数据--》',type,date)	 //arguments?
	}
    
	//使用钩子函数 
	componentDidMount(){	//在这个函数中我们需要
		//订阅了yyy事件 刚开始yyy事件不会触发 一旦触发了yyy事件 就会执行第二个回调函数
		PubSub.subscribe('yyy',this.getMsg2);
	}

	render(){
		return(
			<div>
				<button onClick={this.sendMsg}>点击发送数据给son1组件</button>
				<div>我是son2组件 数据---》：{this.state.msg}</div>
			</div>
		)
	}
}
```

## React CSSTransition 组件

#### 动画组件

引入React动画的cdn

```html
<!-- react动画  让网页更加活力-->
<script src="https://cdn.bootcss.com/react-transition-group/4.3.0/react-transition-group.js"></script>
```

对应的css样式类名（默认的）

```css
/*主动动画的入场 添加的类名*/
/*动画刚入场 添加的类名*/
.appear{ /*写样式*/}
/*动画入场 中 添加的类名*/
.appear-active{/*样式*/}
/*动画入场结束后的样式 添加的类名*/
.appear-dnoe{/*样式*/}


/*动画刚入场 添加的类名*/
.enter{ /*写样式*/}
/*动画入场 中 添加的类名*/
.enter-active{/*样式*/}
/*动画入场结束后的样式 添加的类名*/
.enter-dnoe{/*样式*/}

/*动画刚退场 添加类名*/
.exit{/*样式*/}
/*动画退场 中 添加的类名*/
.exit-active{/*样式*/}
/*动画退出场结束后的样式 添加的类名*/
.exit-done{/*样式*/}

```

结构赋值得到组件

```jsx
const {CSSTransition} = ReactTransitionGroup;
```

默认的属性

1. timeout 毫秒数
2. in 布尔值 true表示动画入场 反之false 动画退场
3. onEnter 监听动画入场时
4. appear 布尔值 是第一次动画的开始
5. onExit 监听动画退出时

#### 一组动画案例

```jsx
const {CSSTransition} = ReactTransitionGroup;
console.log(ReactTransitionGroup);
class App extends React.Component{
	state = {
		isShow:true,
	}
	handleClick =()=>{
		//setState 函数
		//什么时候使用对象形式 改变的属性和改变的属性没有关系
		//什么时候用函数形式  改变的属性和改变前有关系
		//当返回的是一个的对象是要加括号 不然会被解析成方法体 ({对象属性:数据})
		this.setState(state=>({isShow:!state.isShow}))
	}
	
	onEnter =() =>{
		
	}
	onEntering =() =>{
		
	}
	onEntered =(dom) =>{
		dom.style.backgroundColor='pink'
	}
	
	
	onExit =() =>{
		
	}
	onExiting =() =>{
		
	}
	onExited =(dom) =>{
		dom.style.color='#fff'
		console.log('我动画退出了')
	}
	
	render(){
		return(
			<div>
				<button onClick={this.handleClick}>点击切换</button>
				<CSSTransition
					timeout={1000}
					in={this.state.isShow}
					appear={true}
					
					onEnter={this.onEnter}
					onEntering={this.onEntering}
					onEntered={this.onEntered}

					onExit={this.onExit}
					onExiting={this.onExiting}
					onExited={this.onExited}
				>
					<div>我是切换的元素</div>
				</CSSTransition>
			</div>
		)
	}
}


ReactDOM.render(<App/>,document.getElementById('app'))
```

#### 多组动画的案例

1. 多组动画的不需要设置动画的in属性
2. 当元素挂载到dom树上就是动画的入场
3. 当元素从dom树移出就是动画退场

```jsx
//得到多组动画的组件
const {TransitionGroup} = ReactTransitionGroup;
```

```jsx
const {CSSTransition,TransitionGroup} = ReactTransitionGroup;
console.log(ReactTransitionGroup);
class App extends React.Component{
	state = {
		isShow:true,
		list:['html','css','js','node','react']
	}
	handleClick =()=>{
		const {list} = this.state;
		list.pop();
		this.setState(state=>({
			isShow:!state.isShow,
			list:list
		}))
	}
	
	onEnter =() =>{
		
	}
	onEntering =() =>{
		
	}
	onEntered =(dom) =>{
		dom.style.backgroundColor='pink'
	}
	
	
	onExit =() =>{
		
	}
	onExiting =() =>{
		
	}
	onExited =(dom) =>{
		dom.style.color='#fff'
		console.log('我动画退出了')
	}
	
	render(){
		const {list} = this.state;
		return(
			<div>
				<button onClick={this.handleClick}>点击切换</button>
					<TransitionGroup>
					{
						list.map((item)=>{
							return(
								<CSSTransition
								timeout={1000}
								appear={true}
								key={item}
								onExited={()=>{debugger}}
								>
									<div>{item}</div>
								</CSSTransition>
							)	
						})
					}
					</TransitionGroup>
			</div>
		)
	}
}
```

## React 脚手架

####  react 安装

```
npm i create-react-app -g
```

react 版本

```
create-react-app -V
```

react 启动

```
npm start
```

#### react 项目目录

项目

1. node_modules
2. public

   - index.html
3. src

   - App.js

   - index.js
4. gitgnore
5. package.json
6. package-lock.json
7. README.md

注意:默认的css、json、图片文件可以进行删除

评论案例

```jsx
{
    
    
    
    
    
    
    
    
}
```



## React 路由

#### 路由 是什么

​	路由:是一个映射关系

​	后台路由: 路径和回调函数构成一个映射关系

后台路由的特点是
1. 一定会发起网络请求
2. 一定会刷新页面

前台路由:路由和组件够成映射关系
前台路由的特点是 实现原理H5 的historty.pushState 实现的页面应用叫做 SPA Single Page Application

1. 一定不会发生网络请求
2. 一定不会刷新页面

#### 路由 需要引入相关的包

```js
npm i react-router-dom
```

#### 路由 使用

index.js 文件下 BrowserRouter组件是必须写的 不然无法进行路由

```react
//引入文件
import {BrowserRouter} from 'react-router-dom';
//其他包...

ReactDOM.render(
	(
        <BrowserRouter>
        	<App></App>
        </BrowserRouter>
    ),
    document.getElementById('root')
)
```

#### 路由 NavLink 组件

```jsx
//使用NavLink组件
import {NavLink} from 'react-router-dom';
```

```react
<NavLink to="/home">首页</NavLink>

//NavLink 必须写的属性 to  反之报错
//to 属性是写的对应的路由
//NavLink 与 a 标签触触发条件一样 点击被标签包裹的文字
//NavLink 到原生dom中 会被解析成为 a标签

```

​	 路由匹配规则：包含匹配  /home/index 会响应Route的path 中两个路由 /home  /home/index

#### 路由 Route 组件

```react
//使用NavLink,Routem组件
import {NavLink,Route} from 'react-router-dom';
```

```react
//NavLink 和 Routem 组件可以进行配合 一个触发路由 一个触发被路由对应的组件 二者通过路由进行联系
//简单来说就是混合双打
reder(){
	return(
        <NavLink to="/home"></NavLink>
        <Route path="/home" exact component={Home}></Route>
        <Route path="/home/index" component={Home}></Route>
	)
}
//Routem 必须写属性 path component 反之报错
//path 属性 可以写字符串的路由
//component 属性 写组件名 前提先引入响应的组件
//exact属性 可以进行精致匹配

```

#### 路由 Switch 组件

```jsx
//使用NavLink,Route,Switch 组件
import {NavLink,Route,Switch} from 'react-router-dom';
```

```jsx
//NavLink 和 Routem 和 Switch组件可以进行配合 
//NavLink触发路由(NavLink), 
//Routem触发被路由对应的组件(Routem), 
//Switch会把第一个触发路由Routem进行组件响应
//三者通过路由进行联系
//简单来说就是混合三打
reder(){
	return(
        <NavLink to="/home"></NavLink>
        <Switch>
        	<Route path="/home" component={Home}></Route>
        	<Route path="/home/index" component={Home}></Route>
        </Switch>
	)
}
//Switch 组件会把 从上到下匹配Route的path路由 第一个符合条件的进行组件响应
```

路由 

```jsx
//使用NavLink,Route,Switch,Redirect组件
import {NavLink,Route,Switch,Redirect组件} from 'react-router-dom';
```

```jsx
//Redirect组件不会进行 与其他三个组件不会进行混合四打，因为它作用是专治各种不服的熊孩子
//Redirect 就是给熊孩子使用， 当遇到用户在浏览器url地址栏中瞎输入路由时 这个组件就触发 进行重定项
// Redirect 组件专治各种不服
reder(){
	return(
        <NavLink to="/home"></NavLink>
        <Switch>
        	<Route path="/home" component={Home}></Route>
        	<Route path="/home/index" component={Home}></Route>
            <Redirect to="/" component={Home} />
        </Switch>
	)
}
//当用户访问某界面时，该界面并不存在，此时用Redirect重定向，重新跳到一个我们自定义的组件里
```



#### 路由 方法

```

```




## React  redux

####     redux 创世

>  	Redux由Dan Abramov在2015年创建的科技术语。是受2014年Facebook的Flux架构以及函数式编程语言Elm启发。很快，Redux因其简单易学体积小在短时间内成为最热门的前端架构。 

#### [redux 官网](http://cn.redux.js.org/)

#### redux 安装 

```npm
npm i redux  //同步
npm i reudx-thunk //异步
```

####  redux 使用

在src 文件夹中创建一个redux文件件，这个文件中有四个js文件 redux.js store.js actions.js actions-type.js

 store

```javascript
import {createStore,applyMiddleware} from 'redux';
import reducer from 'reducer';
import thunk from 'redux-thunk';
//createStore方法是创建仓库 redcer是数据
//applyMiddleware(thunk)  redux使用thunk这个插件 来扩展redux的功能 异步改变store
//如果没有写这个applyMiddleware(thunk)  异步就会报错,因为只能写对象形式的返回值
export default createStore(redcer,applyMiddleware(thunk));
```

reducer

定义了一些 根据store的老state和action

```javascript
import {ADD,MINUS} from './actions-type';
export default function (state=0,action){ //初始化 state仓库数据 action动作
    switch(action.type){
        case ADD:
            return state+action.data;
        case MINUS:
            return state-action.data;
        default:
            return state; 
    }
    return state; //返回数据，
}
```

actions

   动作都放在这里

```react
import {ADD,MINUS} from './actions-type';

//定义增加仓库数据的action
export const addAction = (value)=>({type:ADD,data:value});

//定义减少仓库数据的action
export const minusAction = (value)=>({type:MINUS,data:value});

//定义增加仓库数据异步action 异步action是一个函数
export const addAsyncAction = (value)=>{
    return dispatch=>{
        setTimeout(()=>{
            dispath(addAction(value))
        },2000)
    }
}

```

actions-type

 这个js文件是暴漏动作的常量 避免字符串会导致程序的不对

```react
export const ADD = 'add';
export const MINUS = 'minus';
```

index

```react
import React from 'react';
import ReactDom from 'react-dom';
import App from './APP';
import store from './redux/store'; //引入redux的store 就是把仓库引入
ReactDOM.render(<App store={store}/>,document.getElementById('root');
//subscribe 的回调函数 是在仓库数据变化时 就触发
store.subscribe(function(){
    ReactDOM.render(<App store={store}/>,document.getElementById('root');
}
//封装redner 方法 
//render = ()=>ReactDOM.render(<App store={store}/>,document.getElementById('root')
//store对象里有四个方法 对数据使用
//1.getState() 方法是获取数据
//2.dispath({type:'命名动作',data:变量})触发一个action(动作用对象的形象表达) 这个动作可以改变仓库中的数据
//3.store.subscribe(function(){}) 仓库中的数据变化就会执行

```

App

```react
import React,{Component} from 'react';
import {addAction,minusAction,addAsyncAction} = './redux/actions'
export default class App extends Component{
  constructor(props){
    super(props)
    this.dom = React.createRef()
  }
  //增加
  add = ()=>{
    const value = +this.dom.current.value; //+this.dom.current.value 把字符串类型隐式转换为整数型

    //触发一个action 这个action 可以改变仓库中的数据
    this.props.store.dispatch(addAction(value))
  }
  //减少
  minus = ()=>{
    const value = +this.dom.current.value; //+this.dom.current.value 把字符串类型隐式转换为整数型
    //触发一个action 这个action 可以改变仓库中的数据
    this.props.store.dispatch(minusAction(value));
  }
  //异步
  addAsync = ()=>{
    const value = +this.dom.current.value; //+this.dom.current.value 把字符串类型隐式转换为整数型
    this.props.store.dispatch(addAsyncAction(value));
  }
   render(){
       //this.props.store.getState() 是获取仓库的数据
       return(
           <div>
           	   	<div>{this.props.store.getState()}</div>
                 <select ref={this.dom}>
                    <option value='1'>1</option> 
                    <option value='2'>2</option> 
                    <option value='3'>3</option> 
                 </select>
                 <button onClick={this.add}>增加</button>
                 <button onClic={this.minus}>减速</button>
           </div>     
       )
   }
}
```

安装 react-redux

```js
npm i react-redux
```

index.js

```react
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import store from './redux/store'; // 引入redux的store
import {Provider} from 'react-redux'; //引入react-redux

ReactDOM.render(
    <Provider store={store}>
        <App/>
    </Provider>, 
    document.getElementById('root'));
```

App.js

```react
import React,{Component} from 'react';
import {addAction,minusAction,addAsyncAction} from './redux/actions';
import {connect} from 'react-redux';
class App extends Component{
  constructor(props){
    super(props)
    this.dom = React.createRef()
  }
  add = ()=>{
    const value = +this.dom.current.value; //+this.dom.current.value 把字符串类型隐式转换为整数型

    //触发一个action 这个action 可以改变仓库中的数据
    // this.props.store.dispatch(addAction(value))
    this.props.add(value);
  }
  minus = ()=>{
    const value = +this.dom.current.value; //+this.dom.current.value 把字符串类型隐式转换为整数型
    //触发一个action 这个action 可以改变仓库中的数据
    // this.props.store.dispatch(minusAction(value))
    this.props.minus(value);
  }
  addAsync = ()=>{
    const value = +this.dom.current.value;
    this.props.addAsync(value);
    // this.props.store.dispatch(addAsyncAction(value))
  }
  render(){
    return(
      <div>
        {/* <div>当前number:是{this.props.store.getState()}</div> */}
        <div>当前number:是{this.props.number}</div>
        <select ref={this.dom}>
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>
        <button onClick={this.add}>点击增加</button>
        <button onClick={this.minus}>点击减少</button>
        <button onClick={this.addAsync}>异步增加</button>
    </div>       
    );
  }
}
function mapStateToProps(state){
  console.log(state,'mapStateToProps函数中打印的');
  return{//这个return 会返回给App组件中， 就是作为<App number={state}/> 一样
    number:state, //把仓库中的state数据映射到number
  }
}
function mapDispatchToProps(dispatch){
  console.log(dispatch)
  return{
    add:(value) =>dispatch(addAction(value)), //把方法映射到App组件中
    minus:(value) =>dispatch(minusAction(value)),
    addAsync:(value)=>dispatch(addAsyncAction(value)),
  }
}
// export default connect(mapStateToProps,mapDispatchToProps)(App)

//简写版
export default connect(
  (state)=>({number:state}),
  {
    add:addAction,
    minus:minusAction,
    addAsync:addAsyncAction,
  })(App)
/*
connect 是连接数据
把store的数据映射成App组件的属性
简化
export default connect(
  (state)=>({number:state}),
  {
    add:addAction,
    minus:minusAction,
    addAsync:addAsyncAction,
  })(App)

*/
```

其余不变

## React 高阶组件

>   **高阶组件（Higher Order Component，HOC）并不是React提供的某种API，而是使用React的一种模式，用于增强现有组件的功能。一个高阶组件就是一个函数，这个函数接受一个组件作为输入，然后返回一个新的组件作为结果，而且，返回的新组件拥有了输入组件所不具备的功能。这里提到的组件并不是组件实例，而是组件类，也可以是一个无状态组件的函数** 

####  高阶组件的意义 

>  **（1）重用代码**。有时候很多React组件都需要公用同样一个逻辑，比如说React-Redux中容器组件的部分，没有必要让每个组件都实现一遍shouldComponentUpdate这些生命周期函数，把这部分逻辑提取出来，利用高阶组件的方式应用出去，就可以减少很多组件的重复代码。
> **（2）修改现有React组件的行为。**有些现成的React组件并不是开发者自己开发的，来自于第三方，或者即便是我们自己开发的，但是我们不想去触碰这些组件的内部逻辑，这时候可以用高阶组件。通过一个独 立于原有组件的函数，可以产生新的组件，对原有组件没有任何侵害。 

#### **高阶组件的实现方式可以分为两大类：**

- **代理方式的高阶组件**
- **继承方式的高阶组件**

**判断条件：**根据返回的新组件和传入组件参数的关系

#### 什么是高阶函数

当一个函数A是接受数参数B时，则函数就是高阶函数

例如 数组中的sort map filter every some 方法

当一个函数A返回函数B时 则函数A就是高阶函数

```js
var arr = new Array(6)
arr[0] = "10"
arr[1] = "5"
arr[2] = "40"
arr[3] = "25"
arr[4] = "1000"
arr[5] = "1"
arr.sort(function sortNumber(a,b){
	return a - b//从小到大
})
```



#### 高阶组件之属性代理

 接受了组件A(基础组件)作为参数并且返回一个组件B的函数

```react
class Input extends Component{
    reder(){
        const {value,handleChange} = this.props
        return <input  {...this.props} type="text">
    }
}
const highOrderCommponent = (BaseComponent)=>{
	//
    return class extends Component{
        state = {
            value:''
        }
        handleChange = e=>{
            this.setState({value:e.target.value})
        }
        render(){
            const {value} = this.state
            const obj = {
              value,
              onChange:this.handleChange
            } 
            return <BaseComponent {...obj}></BaseComponent>
            
        }
    }
}
const Result  = highOrderCommponent(Input)
ReactDOM.render(<Result></Result>,getElementById('box'))            
```

#### 高阶组件之反向继承

```react
class List extends Component{
	state = {
		name:'LongShortParty',
		arr:['html','css','js','node','react']
	}
	render(){
		const {arr} = this.state
		return(
			<ul>
                {
                    arr.map(item=><li key={item}>{item}</li>)
                }
             </ul>
		)
	}
}
const reverseInherit = (BaseComponet)=>{
    return class extends BaseComponet{
        render(){
            console.log(this.state)
            return super.render();
        }
    }
}
const Result1  = reverseInherit(List);
ReactDOM.render(<Result1/></Result1/>,document.getElementById('box'))
```

## 函数组件的hook特性

#### useState函数

userState 也是钩子函数

useState 就是一个hook函数 这个函数可以让函数组件拥有state（状态）

useState(初始值) 返回的是长度为2的数组

第一项的初始值 

第二项是修改初始值的函数

#### useState函数代码示例

```react
const {useState} = React
function YunKong(){
    const [count,setCount] = useState(0) //userState(0)返回是一个数组 这个初始化只用一次
    return(
    	<div>
             我是函数组件
            <p>你已经点击{count}次</p>
            <button onClick={()=>setCount(count+1)}>点击增加</button>
        </div>
    )
}
ReactDOM.render(<YunKong></YunKong>,document.getElementById('box'))
//setCount执行 会重新执行YunKong这个函数
```

#### 多个useState函数代码示例

```jsx
const {useState} = React
function YunKong(){
    const [count,setCount] = useState(0) //userState(0)返回是一个数组 这个初始化只用一次
    const [fruit,setFruit] = useState('banana')
    const [name,setName] = useState('yunkong')
    return(
    	<div>
             我是函数组件
            <p>{count}--{fruit}--{name}</p>
            <button onClick={()=>setCount(count+1)}>点击增加</button>
        </div>
    )
}
ReactDOM.render(<YunKong></YunKong>,document.getElementById('box'))
//setCount执行 会重新执行YunKong这个函数
//useState 的每次执行
//useState 执行个数要和以前一样，不然会报错
```

#### useState 受控表单案例

​	useState用来模拟 ES6类组件中setState方法

```jsx
const {useState} = React;
function Yunkong(){
    let [username,setUserName] = useState('');
    let [psd,setPsd] = useState('');
    const handleClik = ()=>{
        console.log(username,psd);
    }
    <div>
         用户名:
    	<input value={username} onChange={(e)=>setUserName(e.target.value)/>
         密码:
         <input value={psd} onChange={(e)=>setPsd(e.target.value)/>
         <button onClick={handleClik}>点击发送数据</button>
    </div>
}
```

#### useRef 非受控表单案例

```jsx
const {useRef} = React;
function Yunkong(){
    const usernameRef  = useRef(); //用useRef()函数生出一个标记
     const psdRef  = useRef(); //用useRef()函数生出一个标记
    const handleClik = ()=>{ //得到用户名和密码
        console.log(usernameRef,psdRef);
        //打印value值 current表示现在的
        console.log(usernameRef.current.value);
        console.log(psdRef.current.value);
    }
    <div>
         用户名:
    	<input type="text" ref={usernameRef}/>
         密码:
         <input type="password" ref={psdRef} />
         <button onClick={handleClik}>点击发送数据</button>
    </div>
}
```

#### useEffect 代码示例

 useEffect 用来模拟 es6类组件生命周期函数

ussEffect(回调函数,[])

componentDidMount 页面渲染 执行

componentDidUpdate 数据更新 执行

componentWillUnmount

回调函数当前页面渲染render之后 就执行

回调函数一般是写副作用代码

副作用指是

1. 请求数据
2. 修改原生dom

```jsx
const {useEffect,useState} = React
function YouKong(){
    let [count,setCount] = useState(0)
    useEffect(()=>{
        document.title = `你已经点击${count}`
    })
    return(
    	<div>
        	<button onClick={()=>setCount(count+1)></button>
        </div>
    )
}
```

```react
<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="Generator" content="EditPlus®">
  <meta name="Author" content="">
  <meta name="Keywords" content="">
  <meta name="Description" content="">
  <title>Document</title>
 </head>
 <body>
   <div id="box"></div>
	<script type="text/javascript" src="./js/react.development.js"></script>
	<script type="text/javascript" src="./js/react-dom.development.js"></script>
	<script type="text/javascript" src="./js/babel.js"></script>
	<script type="text/babel">
	
	const {useState,useEffect} = React;
	function YunKong(){
		const [color,setColor] = useState('green');
		const [number,setNumber] = useState(0);
		//useEffect 第二个参数 控制下次回调函数的执行
		useEffect(()=>{
			console.log('执行');
			const timer = setInterval(()=>{ //定时器会叠加的
				const randomColor  = '#'+Math.random().toString(16).slice(2,8)
				setColor(randomColor);
			},1000);
			return function(){ //模拟了ComponentWillUnmount
				// 除了第一次render不执行 其他时候都是在render之后执行
				// 执行时间早于useFeect的回调函数
				clearInterval(timer);
			}
		},[number])
		return(
			<div style={{background:color,padding:50,textAlign:'center'}}></div>
		)
		
	}

	ReactDOM.render(<YunKong/>,document.getElementById('box'));
	</script>
 </body>
</html>

```

#### 自定义hook函数

自定义hook 是个函数 一般命名是以use开头

自定义hook函数的作用 管理多个组件的公共状态和公共逻辑

```react
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div id="box"></div>
	<script type="text/javascript" src="./js/react.development.js"></script>
	<script type="text/javascript" src="./js/react-dom.development.js"></script>
	<script type="text/javascript" src="./js/babel.js"></script>
	<script type="text/babel">
		const {useState} = React;

		/*
			自定义hook 是个函数 一般命名是以use开头 一般把组件的公共状态抽离出来
		
		*/
		const useRandomColor = (initColor)=>{
			const [color,setColor] = useState(initColor)
			const handleRandom = ()=>{
				const randomColor = '#' + Math.random().toString(16).slice(2,8);
				setColor(randomColor);
			}
			return [color,handleRandom];
		} 
		function YunKong(){
			const [color,handleRandom] = useRandomColor('red')
			return(
				<div style={{backgroundColor:color,padding:50,textAlign:'center'}}>
					<button onClick={handleRandom}>点击切换颜色</button>
				</div>
			)
		}
		function YunKong2(){
			const [color,handleRandom] = useRandomColor('green')
			const handleClick = ()=>{
				setInterval(handleRandom,1000);
			}
			return(
				<div style={{backgroundColor:color,padding:50,textAlign:'center'}}>
					<button onClick={handleClick}>点击切换颜色</button>
				</div>
			)
		}
		ReactDOM.render( 
			<div>
				<YunKong/>
				<YunKong2/>
			</div>
		,document.getElementById('box'))
	</script>
</body>
</html>
```

useReducer





useContext

