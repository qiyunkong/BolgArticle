### 1. 插值符号
>可以通过{{}} 这样的格式获取Vue里面data的数据， 花括号里可以写js逻辑代码

```html
    <div id="app">
        {{text}} <!-- 通过插值符号可以获取data里面的数据 -->
    </div>

    <script>
        let v = new Vue({
            el: '#app', //挂载的DOM元素，这里表示挂载到ID为app的元素上面
            data: { // 组件数据
                text: 'hello world'
            }
        })
    </script>
```
### 2. v-text
>相当于innerText，在标签节点中添加文本内容， 不能解析HTML标签,v-开头的是vue指令，=号后面引号表示注入的是data中对应的数据，注意: 使用了v-text指令的标签节点里内容不会被渲染
```html
    <div id="app">
        <h2 v-text='text'></h2> <!--直接把text的内容当做字符串显示出来-->
        <p v-text='text'>标签里面的内容</p> <!-- 标签里的内容不会渲染-->
    </div>

    <script>
        let v = new Vue({
            el: '#app',
            data: {
                text: '文本内容'
            }
        })
    </script>
```
### 3. v-html
>相当于 innerHtml 在标签节点中添加HTML内容，可以解析HTML标签，使用了v-html指令的标签节点里的内容也不会被渲染
```html
    <div id="app">
        <p v-html='html'></p> <!--会把html 的内容解析成html-->
        <p v-html=`html`></p> <!--使用反引号表示输入的是字符串内容（页面渲染的是反引号里的字符串）-->
        <p v-html=`${html}`></p> <!--反引号中可以通过$符号来引用data中的数据-->
        <p v-html='html'>节点里的内容</p> <!--节点里的内容也不会被渲染-->
    </div>

    <script>
        let v = new Vue({
            el: '#app',
            data: {
                html: '<strong>hello world</strong>'
            }
        })
    </script>
```
### 4. v-show
>值为false时相当于display:none 用于控制元素在页面中的显示，值应为boolean类型
```html
    <div id="app">
        <h2 v-show='vShow'>hi world</h2>
        <hr>
        <p>{{text}}</p>
    </div>

    <script>
        let v = new Vue({
            el: '#app',
            data: {
                text: '文本内容',
                vShow: false //false 表示不显示，相当于display:none,true显示
            }
        })
    </script>
```
### 5. v-if v-else-if v-else
>相当于if, else if, else 表示满足某个条件才会进行显示该项，当不显示时，是整个元素都不存在，不像v-show会变成display:none。控制多个元素的渲染，可以通过template标签
```html
    <div id="app">
        
        <p v-if='sex === "girl"'>hi girl</p>
        <!-- <p>巴拉巴拉</p> --> <!-- if else 必须连续, 如果中间插入了别的元素,会导致上下判断失败 -->
        <p v-else-if='sex === "boy"'>hi boy</p>
        <p v-else=''>哇</p> <!--假如前面if条件都不成立,v-else写不写内容都会显示-->
        
        <hr>
        <!--控制一组元素的渲染可以通过template 标签-->
        <template v-if="loginType === 'username'">
            <label>用户名</label>
            <input placeholder="请输入用户名" key='1'> 
            <!-- 添加key属性可以让input跟随切换重新渲染,否则切换时,input框引用的还是原来的内容-->
        </template>
        <template v-else>
            <label>密码</label>
            <input placeholder="请输入密码" key='2'>
        </template>
        <button @click='handleClick'>切换</button>
    </div>

    <script>
        let v = new Vue({
            el: '#app',
            data: {
                sex: '1'，
                loginType: 'username'
            },
            methods: {
                handleClick() {
                    if (this.loginType === 'username') {
                        this.loginType = 'password'
                    } else {
                        this.loginType = 'username'
                    }
                }
            },
        })
    </script>
```

> * 当需要频繁的切换dom元素的显示时使用v-show  节省频繁创建dom 销毁dom元素的开销

### 6. v-for
>遍历，可以遍历数组和对象、字符串，数字， 
>* 遍历数组时，参数1为数组项，参数2为索引
>* 遍历对象(json)时，参数1为属性值内容，参数2为属性键名，参数3位索引
>* 遍历数字时， 参数1为数字， 参数2为索引
>* 遍历字符串时， 参数1为字符，参数2为字符的索引
```html
    <div id="app">

        <ul>
            <!-- 遍历数组 key属性尽量不要使用index，重新排列时会引起渲染错位问题 -->
            <li v-for="(item, index) in arr" :key="item">{{index}} - {{item}}</li>
            <!-- 遍历对象 -->
            <li v-for="(value, key, index) in obj" :key="key">{{key}}: {{value}} : {{index}}</li>
        </ul>

    </div>

    <script>
        let v = new Vue({
            el: '#app',
            data: {
                arr: ['html', 'js', 'css', 'vue', 'react'],
                obj: {
                    id: 1,
                    name: '二哈',
                    age: 2,
                    sex: 'girl'
                }
            }
        })
    </script>
```
> ##### v-for 的优先级比 v-if 更高， 不推荐同时使用于同一元素上，可通过computed属性进行类似处理

### 7. v-on
>用于绑定事件,格式v-on:event='function' 或者简写@event
```html
    <div id="app">
        <h2>{{num}}</h2>
        <!-- 通过v-on:event='function' 这个的格式进行绑定事件 -->
        <button v-on:click='handleAdd'>增加</button>
        <!-- v-on:event 可简写成@event的形式 -->
        <button @click='handleMinus'>减少</button>
        <!-- 可以在事件名后面添加修饰词来对事件做一些控制,例如.once表示只能点击一次 -->
        <button @click.once='handleAdd'>增加(仅一次有效)</button>
        <!-- keyup按键事件,.enter表示按下回车键才触发该事件 -->
        <input type="text" @keyup.enter='handleEnter'>
        <!-- v-on可绑定多个事件,v-on的值必须为JSon对象,其中key为事件名,value为对应的事件函数 -->
        <button v-on="{click:handleAdd,mouseenter:handleEnter}">多事件</button>
        <!-- @submit.stop.prevent 阻止默认行为以及阻止冒泡事件(如下,点击后无法跳转到百度了) -->
        <form action="https://www.baidu.com" @submit.stop.prevent>
            <input type="submit" value="提交按钮">
        </form>
        
        <!-- 也可以使用对象语法 (2.4.0+) -->
        <button v-on="{ mousedown: doThis, mouseup: doThat }"></button>
    </div>

    <script>
        let v = new Vue({
            el: '#app',
            data: { //数据选项
                num: 0
            },
            methods: { //方法选项（存放事件函数）
                handleAdd: function () {
                    this.num++
                },
                handleMinus: function () {
                    this.num--
                },
                handleEnter() { //可用ES6的方式定义
                    console.log('hello');
                },
                doThis(){
                    console.log('doThis')
                },
                doThat(){
                    console.log('doThat')
                }
            },
        })
    </script>
```
> ##### 事件修饰符:
> * .stop       阻止事件传播   相当于e.stopPropagation
> * .capture    该事件处理函数在事件捕获阶段触发
> * .prevent    阻止默认行为   相当于e.preventDefault
> * .once       事件处理函数只执行一次
> ##### 按键修饰符:（可以使用keycode,括号里keycode值）
> * .enter(13)      回车事件
> * .space(32)      空格事件
> * .esc           退出事件
> * .delete(8)     delete、退格事件
> * .up(38)/down(40)/left(37)/right(39) 上下左右方向键事件
> * .meta       功能事件(window系统下是window键，mac下是command键）


### 8. v-bind
>v-bind:attr='' 可实现动态绑定属性，attr即需要绑定的属性，''号里面的内容会变成一个变量，表示引入vue应用中的data数据， 可简写成 :attr='' 的格式
```html
    <div id="app">
        <!-- 通过v-bind:attr='' 动态绑定src属性 -->
        <img v-bind:src="img" alt="">
        <!-- 也可以通过 :attr='' 的方式进行绑定 -->
        <img :src="img" alt="">
        <!-- 双重引号可以使用字符串 -->
        <img v-bind:src="'1.jpg'" alt="">
        <!-- 可以使字符串拼接形式,其中name为变量,'.jpg'为字符串 -->
        <img :src="name + '.jpg'" alt="">
        <!-- 可通过反引号的形式引用变量 -->
        <img :src="`${name}.jpg`" alt="">

        <!--样式绑定： style和对象绑定在一块-->
        <div :style=styleObj>{{text}}</div>
        <!--样式绑定： style和数组绑定在一块-->
        <div :style=styleArr>{{text}}</div>

        <!--class和字符串绑定在一块-->
        <div :class="'test'">{{text}}</div>
        <!--class和数组绑定在一块 把数组成员作为标签的类名-->
        <div :class="classArr">{{text}}</div>
        <!--class和对象绑定在一块  如果对象的属性值为true 则属性名会作为标签的类名-->
        <div :class="classObj">{{text}}</div>
    </div>

    <script>
        let v = new Vue({
            el: '#app',
            data: { //数据对象
                name: '1',
                text: '文本内容',
                img: '1.jpg',
                styleObj: {
                    backgroundColor: "lightblue",
                    color: "pink"
                },
                styleArr: [
                    {
                        backgroundColor: "blue",
                        fontSize: "20px"
                    },
                    {
                        color: "grey"
                    }
                ],
                classArr: ['test', 'version'],
                classObj: {
                    show: true,
                    isActive: true
                },

            }
        })
    </script>
```
### 9. v-pre
>v-pre 可以阻止其子元素中的vue指令执行
```html
    <div id="app">
        <h2>{{des}}</h2>
        <div v-pre>
            <!-- v-pre 会阻止其子元素的vue 指令执行 -->
            <h3 v-text="msg"></h3> <!-- 此时只有一个空的h3标签 -->
            <h4>{{title}}</h4> <!-- 此时h4标签内容为字符串'{{title}}' -->
        </div>
        {{title}}
        <!-- 外面的不会被阻止,还是可以引用data中的title数据 -->
    </div>

    <script>

        let vm = new Vue({
            el: '#app',
            data() {
                return {
                    des: 'v-pre',
                    msg: 'hello vue',
                    title: 'this is title'
                }
            },
        })
    </script>
```
### 10. v-cloak
>当在使用{{}} 双花括号进行插值时，如果浏览器频繁刷新页面， vue还没来得响应时，会出现{{xx}}的字符串；因此为了避免这种情况出现，可以使用v-cloak
```html
    <style>
        [v-cloak]{
            display: none;
        }
    </style>
    <div id="app" v-cloak> <!-- v-cloak 配合上面样式,可解决下面问题 -->
        <h2 v-text="title"></h2>
        <p>{{msg}}</p> <!-- 频繁刷新时可能会出现字符串{{msg}}, 而不是内容hello vue -->
    </div>

    <script>

        let vm = new Vue({
            el: '#app',
            data() {
                return {
                    msg: 'hello vue',
                    title: 'this is title'
                }
            },
        })
    </script>
```
### 11. v-model 
>可以实现表单输入框和Vue的数据双向绑定,当data中的数据修改时，表单值同步变化，同理表单修改时，data中的数据也会同步变化
```html
    <div id="app">
        <!-- v-model 实现了表单内容和data的数据绑定 -->
        <p>表单输入框</p>
        <input type="text" v-model='text'>
        <span>{{text}}</span>
        <p>文本域</p>
        <textarea v-model="longText"></textarea>
        <span>{{longText}}</span>
        <p>单选框, 你选中的是{{radioV}}</p>
        <input type="radio" id='vue' value="vue" v-model="radioV">
        <label for="vue">Vue</label>
        <input type="radio" id='react' value="react" v-model='radioV'>
        <label for="react">React</label>
        <p>单个复选框, 状态: {{oneBox}}</p>
        <input type="checkbox" id='oneBox' v-model='oneBox'>
        <label for="oneBox">是/否</label>
        <p>多个复选框, 你选中了: {{checks}}</p>
        <input type="checkbox" id="h5" v-model='checks' value="H5">
        <label for="h5">H5</label>
        <input type="checkbox" id="java" v-model='checks' value="Java">
        <label for="java">Java</label>
        <input type="checkbox" id="golang" v-model='checks' value="goLang">
        <label for="golang">goLang</label>
        <p>下拉选择, 你选的省份是: {{province}}</p>
        <select name="province" v-model='province'>
            <option value="广东">广东</option>
            <option value="北京">北京</option>
            <option value="上海">上海</option>
        </select>
        <p>修饰符</p>
        <p>.lazy</p>
        <!-- 在默认情况下， v-model 在 input 事件中同步输入框的值与数据(即每输一个字符同步一个字符)，
        但可以添加一个修饰符 lazy ，从而转变为在 change 事件中同步,即全部输完后才同步 -->
        <input v-model.lazy="msg"><span> 你输入的内容: {{msg}}</span>
        <p>.number</p>
        <!-- 默认情况下, type="number" 的输入框收集的数字实际会被转为字符串类型的,
        如果想自动把收集到的数据变为真正Number类型,则可以使用.number 修饰符 -->
        <input v-model.number='age' type="number"> {{age}}
        <p>.trim</p>
        <!-- 自动过滤输入的首尾空格 -->
        <input v-model.trim='content'> <span>输入的内容:{{content}};</span>
    </div>

    <script>
        let vm = new Vue({
            el: '#app',
            data: {
                text: '文本内容',
                longText: '文本域内容',
                radioV: 'vue',
                oneBox: true,
                checks: [],
                province: '上海',
                msg: '',
                age: 0,
                content: ''
            }
        })
    </script>
```

### 12. 自定义指令 Vue.directive
>自定义指令，可通过directive进行自定义一个指令，并赋予指令更多的功能
```html
    <div id="app">
        <!-- 通过v- 加自定义指令名称来执行指令相关功能 -->
        <h3 v-custom-command='des'></h3>
        <!-- 指令名称定义为驼峰表示法,在使用指令时需要把大写改成小写,然后使用-连接 -->
        <p v-font-size='"58px"'>自定义指令(全局)</p>

        <p v-color='pink'>自定义指令(局部)</p>
        <p v-background-color='"lightblue"'>自定义指令(局部)</p>
    </div>

    <script>

        // 通过directive自定义指令(全局指令), 并赋予自定义指令对应的功能
        // 如果只是绑定bind钩子,可以简写成如下:
        Vue.directive('custom-command', function (el, binging) {
            console.log(el, binging); //el是使用指令的DOM节点, binging是绑定的对象
            el.innerHTML = binging.value //把binging绑定的值赋予el的innerHTML展示
            el.style.color = 'pink' //赋予更多功能,例如添加颜色或者背景等
            el.style.backgroundColor = 'blue'
        })

        // 完整的写法: (注意,指令名称定义为驼峰表示法,在使用指令时需要把大写改成小写,然后使用-连接)
        Vue.directive('fontSize', {
            // (bind,inserted,update,componentUpdated为自定义指令的生命钩子)
            bind(el, binging) {
                el.style.fontSize = binging.value
            },
            inserted() {
                // todo
            }
        })

        let vm = new Vue({
            el: "#app",
            data() {
                return {
                    des: '自定义指令(全局)',
                    pink: 'pink'
                }
            },
            // 通过directives 自定义局部指令(bind,inserted,update,componentUpdated为自定义指令的生命钩子)
            directives: {
                color: {
                    bind(el, binging) {
                        // 绑定指令时执行
                        console.log('bind执行')
                        el.style.color = binging.value
                    },
                    inserted(el, binging) {   //指令绑定元素上树后执行
                        console.log('inserted执行')
                    },
                    update() { // 元素更新时执行
                        console.log('update执行')
                    },
                    componentUpdated() { //元素更新完执行
                        console.log('componentUpdated执行')
                    }
                },
                // 如果只是绑定bind钩子,可以简写成如下:
                backgroundColor(el, binging) {
                    el.style.backgroundColor = binging.value
                }

            }
        })
    </script>
```