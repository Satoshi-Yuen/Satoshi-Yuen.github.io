---
title: vue基础Ⅰ
date: 2021-01-12 17:03:53
tags:
- vue
---
这是关于vue基础课程实训的课后总结

一、准备工作
1、安装npm工具；
2、安装开发环境(vscode等)；
3、npm上安装模块；
4、vscode安装插件(有需要)；

二、基本使用
1、引入vue.js库（路径因情况而异）
```html
<script src="./node_modules/vue/dist/vue.js"></script>
```
2、使用语法：
（1）script标签内使用new Vue()实例化Vue应用程序element选项，指定被Vue管理的Dom节点入口，值为选择器，必须是一个普通的html节点（不能是html或body），代码具体如下：
```JavaScript
		new Vue({
            el:'#test',
            data:{
                
            },
            methods:{
            
            }
        })
```
（2）在标签体显示数据：{{ 数据名 }}（必须是已被实例化定义的）；
例子：
```html
	<!DOCTYPE html>
	<html lang="en">
	<head>
    	<meta charset="UTF-8">
    	<meta name="viewport" content="width=device-width, initial-scale=1.0">
    	<title>Document</title>
    	<script src="./node_modules/vue/dist/vue.js"></script>
	</head>
	<body>
    	<div id="test">
        	{{ msg }}<br>
        	<a :href="url">Satoshis'blog</a><br>
    	</div>
	</body>
```
```JavaScript
	<script>
        var vue=new Vue({
            el:'#test',
            data:{
                msg:'hello world',
                url:'https://satoshi-yuen.github.io',
            }
        })
	</script>
```
效果：
![](4.PNG)

三、一次性插值v-once
v-once可以使得当数据发生变化时，插值处的内容不会被更新；例如
```html
	<div id="test">
        <span v-once>{{ number }}</span>
        <button @click="cli(number)">点我就+1</button>
	</div>
```
```JavaScript
	<script>
        var vue=new Vue({
            el:'#test',
            data:{
                number:1
            },
            methods:{
                cli(number){
                    this.number++;
                    console.log(number);
                }
            }
        })
	</script>
```
效果：
![](5.PNG)

四、输出html指令v-html
语法：v-html='xxxx'；
作用：
若xxxx的内容为html格式的数据，双大括号会转换为普通文本，想要输出真正的html内容，需要使用v-html指令；此机制多用于防止xss攻击：当输出内容中含有script标签时，则不渲染
	xss攻击主要利用JavaScript脚本注入网页中，读取cookie值到黑客服务器，黑客从而可以对账户进行操作；

五、元素绑定指令v-bind
作用：将数据动态绑定到指定的元素上（主要是实现数据的实时修改，不需要写死参数数据）
语法：v-bind:元素属性名="xxxx"
简写格式：:元素属性名="xxxx"

六、计算属性&监听器
1、计算属性computed
	概念：与methods中定义的函数功能类似，但会进行缓存，因而只会在相关响应式依赖发生变化时才会重新运行；
	要点：
	（1）computed选项内默认是只有getter函数（单向绑定）；
	（2）可调加函数使之具有双向绑定功能；
2、监听器watch
	功能与computed相似，但不同的是，当属性数据发生变化时，对应属性的回调函数会自动调用，在函数内部进行计算；

七、class&style绑定v-bind
通过class和style指定样式可以进行数据绑定，
	语法：v-bind:class='表达式'；v-bind:style='表达式'
	简写：:class='表达式'；:style='表达式'
	要点：
	（1）表达式可以是字符串、对象或者数组（不管是字符串、对象还是数组，字段值最终都指向类名）；

八、条件渲染v-if
作用相当于if判断，另外还有v-else、v-else-if、v-show
v-if与v-show比较：
	元素被渲染的时机：
		v-if若初始条件为假，则不渲染，当条件为真时，都会重新渲染条件元素
		v-show在任何条件下，元素都会被渲染，并且只是简单地基于css进行切换
	开销比较：
		v-if具有更高的切换开销；而v-show具有更高的初始渲染开销；
	所以，若需要非常频繁地切换，则使用v-show较佳；若在运行后条件很少改变，则使用v-if较好。

九、列表渲染v-for
用于进行遍历，要点：
    数组遍历，语法：
        v-for="(alias,index) in array"，参数解析：
            （1）alias：遍历获得的元素别名；
            （2）index：数组索引值，从0开始，是可选值；
            （3）of可替代in，效果一样；
    对象属性遍历，语法：
        v-for="(value,key,index) in object"，参数解析：
            （1）value：每个对象的属性值；
            （2）key：属性名，是可选值；
            （3）index：索引值，是可选值；
            （4）of可替代in，效果一样；
	例子：
```html
		<ul>
            <!--数组遍历-->
            <li v-for="(mem,index) in member">
                {{ mem.name }}({{ mem.age }})
            </li>
            <!--对象属性遍历-->
            <li v-for="(value,key,index) in member[0]">
                {{ key }}-->{{ value }}
            </li>
		</ul>
```
```JavaScript
		el:"#test",
        data: {
            member:[
                {"name":"ohno","age":40},
                {"name":"sakurai","age":38},
                {"name":"aiba","age":38},
                {"name":"ninomiya","age":37},
                {"name":"mastsumoto","age":37}
            ]
		}
```
效果：
![](1.PNG)

十、事件绑定处理指令v-on
用于监听DOM事件，处理点击触发的事件，要点：
    语法：
        v-on:事件名="函数名(参数1,参数2...)"，参数可带可不带；
        简写格式：@事件名="函数名(参数1,参数2...)"，参数可带可不带；
	例子: 
```html
<button v-on:click="clickone">点我1</button>
<button @click="clicktwo(2,3)">点我2</button>
```
```JavaScript
	clickone:function(){
		console.log("successful!")
	},
    clicktwo:function(a,b){
        console.log(a,b);
	}
```
效果：
![](2.PNG)

十一、事件修饰符 
    .stop：阻止单击事件继续传播；
    .prevent：阻止事件默认行为；
    .once：点击事件只会发生一次；
    语法：v-on:事件名.事件修饰符 或者 @事件名.事件修饰符
    例子：
```html
	<div @click="test2">
		<!--若不加.stop，点击"test22"按钮后就会触发"test2"事件，加上则阻止"test2"事件的发生-->
		<button @click.stop="test22">阻止stop</button>  
	</div>
	<!--加上.prevent则不会发生页面跳转，仅仅是发生"test3"的点击事件-->
	<a href="https://satoshi.github.io" @click.prevent="test3">点我3</a><br>  
	<button @click.once="only">一次</button>  <!--.once只允许操作一次-->	
```
```JavaScript
	test2(){
		console.log("test2");
	},
	test22(){
		console.log("test22");
	},
	test3(){
		console.log("test3");
	},
	only(){
		console.log("only");
	}
```
效果：
![](3.PNG)

十二、按键修饰符 
常用按键名：.enter、.tab、.space、.delete、.esc、.up、.down、.left、.right
语法：v-on:keyup.按键名 或 @keyup.按键名

表单数据双向绑定v-model
单向绑定：数据改变，视图改变；视图改变，数据不变；
双向绑定：数据改变，视图改变；视图改变，数据也会改变
v-model：用于表单数据的双向绑定，主要的数据场景使用：
    （1）text文本
    （2）textarea多行文本
    （3）radio单选按钮
    （4）checkbox复选框
    （5）select下拉框

十三、过滤器filter
简而言之就是根据某些条件对数据进行处理再返回结果，也就是将某些数据过滤；要点：
1、全局过滤器：可在全局使用；配置语法：
```JavaScript
Vue.filter(过滤器名称,function(参数1,参数2...){
	数据处理逻辑
})
```
2、局部过滤器：仅在当前实例范围内使用；配置语法：
```JavaScript
new Vue({
	filter: {
		过滤器名称: function(参数1,参数2...){
			数据处理逻辑
		}
	}
})
```
    使用语法：
        一般使用：{{需要操作的数据属性名|过滤器名称(参数1,参数2...)}}
        v-bind使用：v-bind:id="属性名|过滤器名称(参数1,参数2...)"

十四、组件化开发
概念：vue中的组件化开发就是将网页中的重复代码抽取出来，封装成一个个可复用的视图组件，然后将这些视图组件拼接在一起构成一个完整的系统，极大提高了开发效率。
1、全局注册
进行全局注册之后，可以在任何vue实例（new Vue）中使用；语法：
```JavaScript
	Vue.component('组件名',{
		template: '定义组件模板', //简而言之就是需要复用的html代码
		data: function(){   //data中必须是一个函数   
			return { }
		},
		// 可选值
		methods: {
            
		},
	})
```
注意：
	（1）组件名可使用驼峰命名法或者横线分隔命名方式；
	（2）但DOM中只能使用横线分隔方式进行引用组件；
	（3）官方强烈推荐组件名字母全小写并且必须包含一个连字符"-"；
2、局部注册
通常将非通用部分注册为局部组件，一般只适用于当前项目；
语法：
```JavaScript
	var 组件名={
		template: '定义组件模板', //简而言之就是需要复用的html代码
		data: function(){   //data中必须是一个函数 
			return { }
		},
		// 可选值
		methods: {
            
		}
	}
```
```JavaScript
	new Vue({
		el: '',
		data: { },
        <!-- 
            key为组件名，value为引用的组件对象（定义的var对象） 
            若key与value名相同，简写为同一个名即可
        -->
		components: {
			'key': value
		}
	})
```
引用组件时可以通过v-bind指令动态赋值；

十五、父子组件间通信
1、通信方式
（1）props：⽗组件向⼦组件传递数据，使用语法；
```JavaScript
const MyComponent={
 	template: '定义组件模板',  //简而言之就是需要复用的html代码
 	props: xxx,
 	components: {

 	}
 }
```
	要点：
		1）以上是一个子组件对象，全局局部均可；
		2）xxx的内容可以有以下3种：
			以数组形式指定传递属性名，例如：props:['id','name','age']；
			以对象形式指定传递属性名和数据类型，例如：props:{id:Number,name:String,age:int}；
			指定属性名、数据类型、必要性、默认值，例如：props:{name:{type:String,required:true,default:'satoshi'}}；
		3）props只用于父组件向⼦组件传递数据；
		4）所有标签属性都会成为组件对象的属性，模板⻚⾯可以直接引⽤；
		5）若需要向⾮⼦后代传递数据，必须多层逐层传递；
		6）兄弟组件间不能直接进行props通信，必须借助⽗组件；
（2）$emit：⾃定义事件，⼦组件触发⽗组件的⽅法；
	要点：
		1）在⽗组件中定义事件监听函数，并在引用⼦组件标签上使用v-on绑定事件监听，例如：<子组件名 @⾃定义事件名=事件监听函数></子组件名>
		2）在⼦组件methods中触发⽗组件的监听事件函数调⽤，例如：
```JavaScript
methods: {
	deleteHobbie(参数1,...){
		this.$emit('⽗组件中⾃定义事件名')
	}
}
```
		3）⾃定义事件只⽤于⼦组件向⽗组件发送消息(数据)；
		4）此种⽅式不能用于隔代组件或兄弟组件间通信；
（3）slot插槽分发内容，主要⽤于⽗组件向⼦组件传递 标签+数据；
	要点：
		1）使用场景⼀般是某个位置需要经常动态切换显示效果；
		2）只能⽤于⽗组件向⼦组件传递 标签+数据；
		3）传递的插槽标签中的数据处理都需要定义所在⽗组件中；
		4）例子：
子组件：
```html
<slot name="插槽名">我是插槽</slot>
```
父组件：
```html
<子组件名><div class="page-header" slot="插槽名">{{数据}}</div></子组件名>
```
2、通信规则
（1）不能在⼦组件中直接修改⽗组件传递的数据
（2）数据初始化时，应该看初始化的数据是否⽤于多个组件中，若需要被⽤于多个组件中，则初始化在⽗组件中；如果只在⼀个组件中使⽤，则初始化在这个要使⽤的组件中；
（3）数据初始化在哪个组件, 更新数据的⽅法函数就应该定义在哪个组件。

十六、非父子组件间通信
1、使⽤相同⽗组件作为通信桥梁；
2、第三⽅PubSubJS，订阅消息（绑定事件监听）发发布消息（触发事件）；

十七、vue实例生命周期
vue实例生命周期分为3个阶段：
1、初始化显示（执行1次）
	beforeCreate()
	created()
	beforeMount()
	mounted()
2、更新显示（执行n次）
	beforeUpdate()
	updateed()
3、销毁vue实例（调用执行vm.$destory()）
	beforeDestory()
	destoryed()
常用的生命周期方法
（1）mounted()：发送ajax请求、启动定时器等异步任务；
（2）beforeDestory()：做收尾工作；如：清除定时器；
