### 1. el 挂载目标

> el 是提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。可以是 CSS 选择器，也可以是一个 HTMLElement 实例。
> 当然也在Vue实例化之后，也可以通过实例vm.$mount()进行挂载

```html
    <div id="app">
        {{text}}
    </div>

    <script>

        let vm = new Vue({
            // el: "#app", //创建一个Vue实例时先不挂载
            data() {
                return {
                    text: '实例挂载',
                }
            },
        })
        // 然后通过实例调用$mount()方法进行挂载
        vm.$mount('#app')

        // 可通过实例.$el进行访问
        console.log(vm.$el)
    </script>
```

### 2. data 数据
> data选项为Vue实例的数据对象，Vue会递归将data的属性转换为getter/setter,从而让data属性的数据能够响应式变化。 注意，属性不能以 _ 或 $ 开头，这些属性不会被Vue实例代理。
> 可以通过实例vm.$data.属性 进行访问数据或者修改数据内容

```html
    <div id="app">
        {{text}}
    </div>

    <script>

        let vm = new Vue({
            el: "#app", 
            data() {
                return {
                    text: '实例挂载',
                }
            },
        })
        vm.$data.text = '新的数据'
        // 可通过实例.$data进行访问
        console.log(vm.$data)
    </script>

```
### 3. methods 方法
> Vue的实例的方法选项， 定义的函数可以通过v-on绑定到元素的事件中

```html
   <div id="app">
        {{number}}
        <button @click='handleClick'>click</button>
        <button @click='handleAdd'>add</button>
    </div>

    <script>

        let vm = new Vue({
            el: "#app",
            data() {
                return {
                    number: 0,
                }
            },
            methods: {
                handleClick() {
                    this.number++
                },
                // 注意: 不应该使用箭头函数,因为箭头函数在定义时就绑定了父级作用域, 所以this的指向不会是vue实例
                handleAdd: () => {
                    console.log(this);// 这里打印的this 是window对象
                }
            },
        })

    </script>
```

### 4. computed 计算属性
>**注意：computed和methods 效果上两个虽然是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。**
```html
    <div id="app">
        <h1>{{des}}</h1>
        <!-- 通过调用computed中的fullName函数获取计算处理后的结果 -->
        <h2>{{fullName}}</h2>
        <h2>{{mFullName()}}</h2>
        <h3>{{say}}</h3>
    </div>

    <script>

        let vm = new Vue({
            el: "#app",
            data() {
                return {
                    des: 'computed 计算',
                    firstName: 'ye',
                    lastName: 'zi',
                    sayContent: 'say hello'
                }
            },
            computed: {
                // 通过computed 实现对data的数据进行特殊计算处理
                fullName() {
                    return this.firstName + ' ' + this.lastName
                },

                // computed 默认只有getter方法,页面直接{{say}},其实就是调用get方法
                say: {
                    get: function () {
                        return this.sayContent
                    },
                    // 当然也可以自定义setter方法,这样页面就可以通过vm.say = '' 
                    // 进行修改say的内容了 否则通过vm.say = 'xx'修改会报错
                    set: function (param) {
                        this.sayContent = param
                    }
                }
            },
            // 当然,也可以通过methods来实现
            methods: {
                mFullName() {
                    return this.firstName + ' ' + this.lastName
                }
            },
        })

    </script>
```

### 5. watch 监听器
```html
    <div id="app">
        <p v-text='count'></p>
        <button @click='add'>增加</button>
        <button @click='minus'>减少</button>
    </div>

    <script>

        let vm = new Vue({
            el: "#app",
            data() {
                return {
                    count: 0,
                    person: {
                        name: 'lance',
                        age: 18
                    },
                    arr: [0, 1, 2]
                }
            },
            methods: {
                add() {
                    this.count++
                },
                minus() {
                    this.count--
                }
            },
            watch: {
                // 通过watch监听count数据,函数名对应监听的数据名,参数1是即将变化的值,参数2是变化前的值
                count(newValue, oldValue) {
                    console.log(newValue, oldValue);
                    if (newValue < 0) {
                        this.count = 0 //控制监听的数据变化最小只能为0
                    }
                    if (newValue > 10) {
                        this.count = 10 //控制监听的数据变化最大只能为10
                    }
                },
                // 上面为简写, 下面是完整的写法
                count: {
                    handler(newValue, oldValue) {  //当count变化时触发
                        console.log(newValue, oldValue)
                    },
                    immediate: true, // 数据初始化时 就执行一次handler函数
                },

                // 监听对象
                person: { //监听person  该监视器 可以监控对象内部任一个属性的变化
                    handler(newValue) {  //当person变化时触发,没有oldValue
                        console.log(newValue)
                    },
                    deep: true, //监控对象属性的改变需要设置,否则无效
                },
                "person.name": { //监听person对象的name属性
                    handler(newValue, oldValue) {  //当name属性变化时触发
                        console.log(newValue, oldValue)
                    },
                    // deep: true, //监控对象的一个属性的改变时可以不设置
                },

                arr() {
                    // 也可以监听数组, 但数组如果通过索引修改的,无法监听!
                    console.log('数组变化了~')
                }
            },
        })
        // 也可以通过调用实例的$watch方法进行监听
        vm.$watch('count', function (newValue, oldValue) {
            console.log(newValue, oldValue);
            if (newValue < 0) {
                this.count = 0
            }
        })
    </script>
```

### 6. filters 过滤器
```html
    <div id="app">
        <!-- 使用过滤器,必须是在{{}}中使用,并通过|表示使用过滤器 -->
        <h3>{{ msg | myFilter}}</h3>
    </div>

    <script>

        let vm = new Vue({
            el: "#app",
            data() {
                return {
                    msg: 'hello world'
                }
            },
            filters: {
                // 通过过滤器,可以对数据进行过滤或者其它处理
                myFilter(value) {
                    return value.split("").reverse().join("")
                }
            }
        })
    </script>
```

### 7 .directives 自定义指令
> 详见 Vue 指令 12点

### 8. template 模板定义
```html
    <div id="app">

    </div>

    <!-- 定义了一个模板, 模板默认在页面是不会解析出标签样式的 display: none; -->
    <template id='tpl'>
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
        </ul>
    </template>

    <script>

        // 通过template属性把ID为tpl的模板进行挂载到app上,此时模板内容就可以被解析了
        let vm = new Vue({
            el: "#app",
            template: "#tpl"
        })
    </script>
```

### 9. component 注册组件
```html
    <div id="app">
        <!-- 使用注册组件 如果为驼峰命名法的时候，在调用时需要使用 - 来隔开; -->
        <a-side-bar></a-side-bar>
        <a-header></a-header>
    </div>

    <script>

        // 全局注册组件 【组件名，组件的方法】
        Vue.component('aSideBar', {
            template: `
                <div>
                    <p>{{des}}</p>
                </div>
            `,
            data() {
                return {
                    des: "注册的组件(全局的)"
                }
            },
        })

        let vm = new Vue({
            el: "#app",
            data() {
                return {
                    msg: 'hello world'
                }
            },
            // 局部组件
            components: {
                aHeader: {
                    template: `
                        <div>
                            <p>{{des}}</p>
                        </div>
                    `,
                    data() {
                        return {
                            des: "注册的组件(局部的)"
                        }
                    },
                }
            }
        })
    </script>
```
### 10. component 组件拓展
```html
    <div id="app">
        <!-- 通过组件名称使用,驼峰命名需要转-连接 -->
        <component-a></component-a>
        <!-- 通过:is 指定组件ID -->
        <component :is="compB"></component>
    </div>

    <script>

        // 定义变量componentA和componentB内容
        let componentA = {
            template: `
                <div>组件A</div>
            `
        }
        let componentB = {
            template: `
                <div>组件B</div>
            `
        }

        let vm = new Vue({
            el: '#app',
            data: {
                // 定义compA变量名, 变量内容为componentB对象(上面定义的)
                compB: componentB
            },
            // 组件集
            components: {
                //定义了名字为componentA的组件,并引用上面的componentA变量内容
                componentA // 实际是 componentA: componentA
            }
        })
    </script>
```