vue init webpack vue-test

var vm = new Vue({
    el: '',
    data: {

    },
    methods: {

    },
    created: {

    }
})

### API
# split() 方法用于把一个字符串分割成字符串数组。
# reverse() 方法用于颠倒数组中元素的顺序。
# join() 方法用于把数组中的所有元素放入一个字符串。
# substring(0,1)   // 字符串截取，从第0个开始，截取1个；
message.split('').reverse().join('')
# array.push()


### Vue.js（读音 /vjuː/, 类似于 view） 是一套 构建 用户界面 的渐进式框架。
### Vue 只关注 视图层， 采用自底向上增量开发的设计。
### Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件。
### Vue.js 模板语法  
Vue.js 使用了基于 HTML 的模版语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。
Vue.js 的核心是一个允许你采用简洁的模板语法来声明式的将数据渲染进 DOM 的系统。
结合响应系统，在应用状态改变时， Vue 能够智能地计算出重新渲染组件的最小代价并应用到 DOM 操作上。

### 基础结构

<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script>
    new Vue({
        el:"#box",
        data:{
            message:"Hello Vue !"
        }
    })
</script>
 
Vue.js 目录结构
目录/文件	    说明
build	        项目构建(webpack)相关代码
config	        配置目录，包括端口号等。我们初学可以使用默认的。
node_modules	npm 加载的项目依赖模块
src	            这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：
    assets: 放置一些图片，如logo等。
    components: 目录里面放了一个组件文件，可以不用。
    App.vue: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。
    main.js: 项目的核心文件。
static	        静态资源目录，如图片、字体等。
test	        初始测试目录，可删除
.xxxx文件	    这些是一些配置文件，包括语法配置，git配置等。
index.html	    首页入口文件，你可以添加一些 meta 信息或统计代码啥的。
package.json	项目配置文件。
README.md	    项目的说明文档，markdown 格式

###   {{ }}  v-html  v-text v-show v-if

### 插值
## 文本:数据绑定最常见的形式就是使用 {{...}}（双大括号）的文本插值
    <div id="box">{{message}}</div>

## Html:使用 v-html 指令用于输出 html 代码
    <div id="box">
        <div v-html = "message"></div>
    </div>

## 属性:HTML 属性中的值应使用 v-bind 指令。(:)
    <div v-bind:class="{'class1': use}">
        v-bind:class 指令
    </div>
## 表达式
    <div id="app">
        {{5+5}}<br>
        {{ ok ? 'YES' : 'NO' }}<br>
        {{ message.split('').reverse().join('') }}
        <div v-bind:id="'list-' + id">菜鸟教程</div>
    </div>
## 指令    指令是带有 v- 前缀的特殊属性     指令用于在表达式的值改变时，将某些行为应用到 DOM 上。
    <div id="app">
        <p v-if="seen">现在你看到我了</p>
        <template v-if="ok">
            <h1>菜鸟教程</h1>
            <p>学的不仅是技术，更是梦想！</p>
            <p>哈哈哈，打字辛苦啊！！！</p>
        </template>
    </div>


### v-show:我们也可以使用 v-show 指令来根据条件展示元素
    <div id="app">
        <h1 v-show="ok">Hello!</h1>
    </div>
        
    <script>
    new Vue({
      el: '#app',
      data: {
        ok: true
      }
    })
    </script>


### 条件语句
v-if
v-if....v-else
v-if....v-else-if....v-else-if....v-else
v-show

### 循环语句 (普通数组、对象数组、对象)
<li v-for="site in sites">{{ site.name }}</li>
<template v-for="site in sites">
  <li>{{ site.name }}</li>
  <li>--------------</li>
</template>
<li v-for="value in object">{{ value }}</li>
<li v-for="(value, key) in object">{{ key }} : {{ value }}</li>
<li v-for="(value, key, index) in object">{{ index }}. {{ key }} : {{ value }}</li>
<li v-for="n in 10">{{ n }}</li>

### Vue.js 计算属性：计算属性关键词: computed。计算属性在处理一些复杂逻辑时是很有用的。
{{ message.split('').reverse().join('') }}

<script>
    var vm = new Vue({
          el: '#app',
          data: {
            message: 'Runoob!'
          },
          computed: {
                // 计算属性的 getter
                reversedMessage: function () {
                      // `this` 指向 vm 实例
                      return this.message.split('').reverse().join('');
                }
          }
    })
</script>

### computed vs methods:我们可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。
可以说使用 computed 性能会更好，但是如果你不希望缓存，你可以使用 methods 属性。




  
React.js    开发网站和手机APP
Vue.js      需要借助也Weex，可以进行APP的开发
Angular.js  

Vue.js 是一套构建用户界面的框架  只关注视图层

1、框架可以提升开发效率
2、原生JS(存在兼容性问题) 
    -> Jquery类库(解决了兼容性问题) 
    -> 前端引擎框架(解决了频繁操作DOM)
    -> Angular.js/Vue.js(减少不必要的DOM操作，只需要关注与业务逻辑，不再关注DOM是如何渲染的)
3、在VUE中，一个核心的概念，就是让用户不在操作DOM元素，解放了用户的双手，让程序员可以风度哦的时间区关注业务逻辑。

### angular
## AngularJS  1.x
## AngularIO

框架 和 库 的区别

框架：是一套完整的解决方案，对项目的侵入性比较大，项目如果需要更换框架，则需要重新架构整个项目；

库(插件)：提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其他库实现需求；

MVC：(M V C)是后端的分层开发概念；

MVVM：(M V VM)是前端视图层的概念，主要关注与视图层分离。

var vm = new Vue({
    el : '#box',
    data : {
        'msg' : 'Hello World'
    }
})

## v-cloak / v-text / v-html
    <p>===={{msg}}====</p>
    <p v-cloak>===={{msg}}====</p>
    <p v-text = "msg"></p>
    <p v-html = "msg"></p>

## v-bind  (可以简写成 : ) 后面可以写合法的表达式   用于绑定属性
    <input type="button" value="按钮" v-bind:title="mytitle">
    <input type="button" value="按钮" :title="mytitle">
    <input type="button" value="按钮" v-bind:title="mytitle + '123'">

## v-on 用于绑定时间 (可以简写成 @ )

    <input type="button" value="按钮2" v-on:click="show">
    methods : {
        show : function(){
            alter("hello world");
        }
    }

## 事件修饰符  .stop  .prevent .capture  .self  .once
.stop       // 阻止冒泡
.prevent    // 阻止默认行为  a form
.capture    // 事件捕捉，从外到里（与事件冒泡相反）
.self       // 只阻止自己，不阻止别人
.once       // 事件只触发一次

## 实现双向数据绑定  v-model
# v-model   v-model=""  
# v-bind    v-bind:title = ""
# v-model 只能运用在表单元素中；
# v-model 可以实现数据的双向绑定
    <input type="text" name="" id="" v-model="msg">
    <input type="button" value="按钮" v-bind:title="mytitle">
    <input type="button" value="按钮" :title="mytitle">
    <input type="button" value="按钮" v-bind:title="mytitle + '123'">

## 样式   v-bind (:)

# class样式

1. 数组
<h1 :class="['red', 'thin']">这是一个邪恶的H1</h1>

2. 数组中使用三元表达式
<h1 :class="['red', 'thin', isactive?'active':'']">这是一个邪恶的H1</h1>

3. 数组中嵌套对象
<h1 :class="['red', 'thin', {'active': isactive}]">这是一个邪恶的H1</h1>

4. 直接使用对象
<h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>

# 内联样式

1. 直接在元素上通过 `:style` 的形式，书写样式对象
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>

2. 将样式对象，定义到 `data` 中，并直接引用到 `:style` 中
 + 在data上定义样式：
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' }
}
 + 在元素中，通过属性绑定的形式，将样式对象应用到元素中：
<h1 :style="h1StyleObj">这是一个善良的H1</h1>

3. 在 `:style` 中通过数组，引用多个 `data` 上的样式对象
 + 在data上定义样式：
data: {
        h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' },
        h1StyleObj2: { fontStyle: 'italic' }
}
 + 在元素中，通过属性绑定的形式，将样式对象应用到元素中：
<h1 :style="[h1StyleObj, h1StyleObj2]">这是一个善良的H1</h1>

## v-for    **当在组件中使用** v-for 时，key 现在是必须的
    <div id="app">
        <!-- 普通数组 -->
        <p v-for="(list,index) in lists">{{ index }} -- {{ list }}</p>
        <!-- 对象数组 -->
        <p v-for="(user,index) in lists2">ID:{{ user.id }} -- 名字:{{ user.name }} -- 年龄:{{ user.age }} -- 索引:{{ index }}</p>
        <!-- 对象 -->
        <p v-for="(value,key,i) in lists3">键:{{ key }} -- 值:{{ value }} -- 索引:{{ i }}</p>
        <!-- 迭代数字 -->
        <p v-for="count in 10">这是第{{ count }} 次循环</p>
    </div>


    <script>
        var vm = new Vue({
            el : '#app',
            data : {
                lists : [1,2,3,4,5,6],
                lists2 : [
                    {id: 1 , name: 'zs' , age: 11},
                    {id: 2 , name: 'ls' , age: 12},
                    {id: 3 , name: 'ww' , age: 13},
                    {id: 4 , name: 'zl' , age: 14},
                ],
                lists3 : {id : 1, name: 'zml', gender: '男' }
            },
            methods : { }
        })
    </script>

## v-if  v-show
# v-if  每次都会重新删除和创建元素，有较高的切换性能消耗
# v-show  不会重新删除和创建元素，只是切换元素的display 样式，有较高的初始渲染消耗
# 如果元素涉及到频繁的操作，最好不要使用 v-if
# 如果元素可能永远也不会显示出来，则推荐使用 v-if







### VUE 生命周期
生命周期钩子 = 生命周期函数 = 生命周期事件

beforeCreate()
created()
beforeMount()
mounted()
beforeUpdate()
updated()



### vue-resource


### 动画

## 使用过度类名实现动画

    <style>
        .v-enter,
        .v-leave-to{
            opacity: 0;
            transform: translateX(200px);
        }
        .v-enter-active,
        .v-leave-active{
            transition:all 0.4s ease;
        }
    </style>

    <transition mode="out-in">
        <h3 v-if="flag">这是一个h3标签</h3>
    </transition>

    data : {
        flag: false,
    },

# 如果transition有那么属性，要通过前缀来单独控制

    <style>
        .my-enter,
        .my-leave-to{
            opacity: 0;
            transform: translateX(200px);
        }
        .my-enter-active,
        .my-leave-active{
            transition:all 0.4s ease;
        }
    </style>

    <transition name="my">
        <h3 v-if="flag">这是一个h3标签</h3>
    </transition>

## 使用钩子函数名实现动画

    <style>
        .ball{
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background-color: red;
        }
    </style>

    <div id="app">
        <input type="button" value="快到碗里来" @click="flag=!flag">
        <transition @before-enter="beforEnter" @enter="enter" @after-enter="afterEnter">
            <div class="ball" v-show="flag"></div>
        </transition>
    </div>

    <script>
        var vm = new Vue({
            el : '#app',
            data : {
                flag: false,
            },
            methods : {
                // 参数 el 表示要执行动画的那个DOM元素，是个原生的 JS DOM 对象
                beforEnter(el){  // 动画入场之前，动画尚未开始，可以在该函数中设置元素开始动画之前的 起始位置
                    el.style.transform = "translate(0, 0)"
                },
                enter(el,done){  // enter 表示动画开始之后的样式，在该函数中设置小球动画之后的 结束状态
                    el.offsetHeight
                    el.style.transform = "translate(150px, 450px)"
                    el.style.transition = "all 1s ease"
                    done()   // done就是afterEnter函数的引用
                },
                afterEnter(el){  // 动画完成之后
                    th is.flag = !this.flag
                }
            }
        })
    </script>

## transition-group


### Vue组件

## 组件的出现就是为了拆分Vue实例的代码量的，能够让我们以不同的组件，来划分不同的功能模块，姜来我们需要什么样的功能，就可以调用相应的组件即可；
模块化：从代码逻辑的角度惊醒划分的；方便代码分层开发，保证每个功能模块的智能单一；
组件快：是从UI界面角度进行划分的，前端的组件化，方便UI组件的重用
# 定义组件的时候，如果要定义全局的组件  Vue.component('组件名称',{})
# 定义私有组件
1、使用Vue.extend 来创建全局的Vue组件
2、使用Vue.component('组件名称',创建出来的组件模板对象)
3、引用组件
    <my-com1></my-com1>
    <script>
        var com1 = Vue.extend({
            template: "<h3>这是使用Vue.extend创建的组件</h3>"
        })
        Vue.component('myCom1',com1)
        
    </script>

# 方法一 如上，还有缩写方式
# 方法二 省略Vue.extend({})   template 直接写在{} 内
# 方法三  template写在script外部

## 定义私有组件

var vm = new Vue({
    el: '',
    data: '',
    methods:{

    },
    filters: {

    },
    components: {    // 私有
        login: {
            template: '#tmpl2'
        }
    }
})

## 组件中的data
data: function(){
    return {}
}


## 切换

1、v-if   v-else

2、<component :is="'login'"></component>

3、通过mode属性




## Vue 标签

component 、 template 、 transition 、 transitionGroup



### 父组件向子组件传值

# 把父组件传递过来的parentmsg属性，先在props数组中定义一下，才能使用这个数据；  props: ['parentmsg]'; 
# props 中的数据，都是只读的，无法重新赋值

# <父组件名 :parentmsg="msg"></父组件名>

子组件中的data数据并不是通过父组件传递过来的，而是子组件自身私有的，比如ajax请求回来的数据，都可以放到data身上

### 父组件向子组件传方法

<com2 @func="show"></com2>

var com2 = {
    template: '#tmpl',
    methods: {
        myclick(){
            this.$emit('func')  // this.$emit 是固定写法， emit ：调用，触发 的意思
        }
    }
}
  
 
### ref 获取DOM元素和组件

<h3 id="myh3" ref="myh3">hahahaha</h3>
console.log(this.$refs.myh3.innerText)


### 路由
## 后端路由：对于普通的网站，多有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源；
## 前端路由：对于单页面应用程序来说，主要通过URL中的hash(#号)来实现不同页面之间的切换，同时，hash有一个特点：HTTP请求中不会包含hash相关的内容，所以，单页面程序中的页面跳转主要用hash实现
 
<div id="app">
    <!-- <a href="#/login">登录</a>
    <a href="#/register">注册</a>
    <router-view></router-view> -->

    <router-link to="/login">登录</router-link>
    <!-- <router-link to="/login" tag="span">登录</router-link> -->   // tag 属性
    <router-link to="/register">注册</router-link>

</div>

var login = {
    template: "<h1>登录组件</h1>"
}
var register = {
    template: "<h1>登录组件</h1>"
}

var routerObj = new VueRouter({
    routes: [
        // component 的属性值必须是一个组件模板对象，不能是组件的引用名称，不能是'login'
        {path: '/', redirect: '/login'},
        {path: '/login', component: login},
        {path: '/register', component: register}
    ]
});

var vm = new Vue({
    el: '',
    data: {

    },
    methods: {

    },
    router: routerObj
})

### Promise
Promise 是一个构造函数  new Promise()
Promise有两个回调函数 resolve()  和 reject()  分别是成功之后调用和失败之后调用
Promise 后遭函数的Prototype属性上，有一个 .then() 方法
Promise 表示一个 异步操作；new一个Promise是实例，这个实例就表示一个具体的异步操作
这个异步操作的结果 只有两种状态
状态1：异步执行成功，需要在内部调用 成功的回调 resolve 把结果返回给调用者；
状态2：异步执行失败，需要在内部调用 成功的回调 reject 把结果返回给调用者；
由于Promise是一个实例，是一个异步操作，所以，内部拿到操作结果之后，无法使用return 吧操作结果返回给调用者，这时候只能使用回调函数的形式，来吧成功 或者 失败的节后返回给调用者
在new出来的Promise实例上，调用 .then() 方法，预先为这个Promise异步操作 指定成功(resolve)和失败(reject)回调函数

var promise = new Promise(function(){
    // 具体的异步操作
})





vue.js
vue-resouece.js
vue-router.js
<label></label>
this.list.some
this.list.foreach
this.list.findIndex
array: push  aplice
jsonp
属性和变量的缩写

列表
小球移动
登录注册

const path = require('path')
const fs = require('fs')

fs.readFile(path.join(__dirname,'./files.txt'),utf-8,(err,data)=>{
    if(err) throw err
    console.log(data)
})






var vm = new Vue({
    el: '',
    data() {
        return {

        }
    },
    methods: {

    }
    created() {

    },
    mounted() {

    }，
    computed: {   // 计算属性(计算属性是基于它们的响应式依赖进行缓存的  )
        reversendMessage() {
            return this.message.split('').reverse().join('')
        }
    },
    watch: {     // 侦听器

    }
})

var routerObj = new VueRouter({
    routes: [

    ],
    linkActiveClass: ''
})


{{  }}
v-html
v-text
v-bind:   (':')
v-on     ('@')

计算属性缓存(computed) VS 方法(methods)

v-if
v-show
当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级



.stop
.prevent
.capture
.self
.once
.passive



### sessionStorage  getItem  setItem  removeItem  clear
sessionStorage.key(int index) //返回当前 sessionStorage 对象的第index序号的key名称。若没有返回null。
sessionStorage.getItem(string key) //返回键名(key)对应的值(value)。若没有返回null。
sessionStorage.setItem(string key, string value) //该方法接受一个键名(key)和值(value)作为参数，将键值对添加到存储中；如果键名存在，则更新其对应的值。
sessionStorage.removeItem(string key) //将指定的键名(key)从 sessionStorage 对象中移除。
sessionStorage.clear() //清除 sessionStorage 对象所有的项。

### QS

方法一：将对象序列化，多个对象之间用 & 拼接（拼接是有底层处理，无需手动操作）
qs.stringfy()  转换成查询字符串
let comments = {content: this.inputValue}
let comValue = qs.stringify(comments)
方法二：将序列化的内容拆分成一个个单一的对象
qs.parse()   转换成json对象

### axios  get  post
## get
axios.get('url',{       // 参数还可以直接拼接在URL后面
    params: {
        title: '眼镜'
    }
}).then(function(res){
    this.goodsList = res.data;
}).catch(function(error){
    console.log(error);
})
## post
axios.post('url',{
    firstName: 'zhang',
    lastName: 'san'
}).then(function(res){
    console.log(res)
}).catch(function(err){
    console.log(error)
})
## post 参数是对象
var params = new URLSearchParams();
params.append('title','眼镜');
params.append('id',1);
axios.post('url',params).then(function(res){

}).catch(function(error){
    
})
## all
function getUserAccout(){
    return axios.get('url');
}
function getUserPermissions(){
    return axios.get('url');
}
axios.all([getuserAccount(), getUserPermissions()])
    .then(axios.spread(function(axxt, perms){
        // 两个请求现已完成
    })
);

