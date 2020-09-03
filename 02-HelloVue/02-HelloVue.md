# （二）HelloVue

## 2.1 HelloVuejs

​ 如何开始学习 Vue，当然是写一个最简单的 demo，直接上代码。此处通过 cdn`<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>`获取 vuejs。

​ vue 是声明式编程，区别于 jquery 的命令式编程。

### 2.1.1 命令式编程

​ 原生 js 做法（命令式编程）

1. 创建 div 元素，设置 id 属性
2. 定义一个变量叫 message
3. 将 message 变量放在 div 元素中显示
4. 修改 message 数据
5. 将修改的元素替换到 div

### 2.1.2 声明式编程

​ vue 写法（声明式）

1. 创建一个 div 元素，设置 id 属性
2. 定义一个 vue 对象，将 div 挂载在 vue 对象上
3. 在 vue 对象内定义变量 message，并绑定数据
4. 将 message 变量放在 div 元素上显示
5. 修改 vue 对象中的变量 message，div 元素数据自动改变

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>
		<title>HelloVuejs</title>
	</head>
	<body>
		<div id="app">
			<h2>{{message}}</h2>
			<p>{{name}}</p>
		</div>
		<script>
			//let变量/const常量
			//编程范式：声明式编程
			const app = new Vue({
				el: '#app', //用于挂载要管理的元素
				data: {
					//定义数据
					message: 'HelloVuejs',
					name: 'zzz',
				},
			});
		</script>
	</body>
</html>
```

​ 在谷歌浏览器中按 F12，在开发者模式中 console 控制台，改变 vue 对象的 message 值，页面显示也随之改变。

​ `{{message}}`表示将变量 message 输出到标签 h2 中，所有的 vue 语法都必须在 vue 对象挂载的 div 元素中，如果在 div 元素外使用是不生效的。`el:"#app"`表示将 id 为 app 的 div 挂载在 vue 对象上，data 表示变量对象。

## 2.2 vue 列表的展示（v-for）

​ 开发中常用的数组有许多数据，需要全部展示或者部分展示，在原生 JS 中需要使用 for 循环遍历依次替换 div 元素，在 vue 中，使用`v-for`可以简单遍历生成元素节点。

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>
		<title>vue列表展示</title>
	</head>
	<body>
		<div id="app">
			<h2>{{message}}</h2>
			<ul>
				<li v-for="(item, index) in movies" :key="index">{{item}}</li>
			</ul>
		</div>
		<script>
			const app = new Vue({
				el: '#app', //用于挂载要管理的元素
				data: {
					//定义数据
					message: '电影列表',
					movies: ['星际穿越', '海王', '大话西游', '复仇者联盟'], //定义一个数组
				},
			});
		</script>
	</body>
</html>
```

显示结果如图所示：

![](.\images\2.2.1-1.png)

​ `<li v-for="(item, index) in movies" :key="index">{{item}}</li>`item 表示当前遍历的元素，index 表示元素索引， 为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一 `key` 属性。建议尽可能在使用 `v-for` 时提供 `key` attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。

因为它是 Vue 识别节点的一个通用机制，`key` 并不仅与 `v-for` 特别关联。

> 不要使用对象或数组之类的非基本类型值作为 `v-for` 的 `key`。请用字符串或数值类型的值。

## 2.3 vue 案例-计数器

​ 使用 vue 实现一个小计数器，点击`+`按钮，计数器+1，使用`-`按钮计数器-1。

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<meta http-equiv="X-UA-Compatible" content="ie=edge" />
		<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>
		<title>vue计数器</title>
	</head>
	<body>
		<div id="app">
			<h2>当前计数：{{count}}</h2>
			<!-- 
      <button v-on:click="count--">-</button>
      <button v-on:click="count++">+</button> 
      -->
			<button v-on:click="sub()">-</button>
			<button @click="add()">+</button>
		</div>
		<script>
			const app = new Vue({
				el: '#app', //用于挂载要管理的元素
				data: {
					//定义数据
					count: 0,
				},
				methods: {
					add: function () {
						console.log('add');
						this.count++;
					},
					sub: function () {
						console.log('sub');
						this.count--;
					},
				},
			});
		</script>
	</body>
</html>
```

1. 定义 vue 对象并初始化一个变量 count=0

2. 定义两个方法`add`和`sub`，用于对 count++或者 count--

3. 定义两个 button 对象，给 button 添加上点击事件

    在 vue 对象中使用 methods 表示方法集合，使用`v-on:click`的关键字给元素绑定监听点击事件，给按钮分别绑定上点击事件，并绑定触发事件后回调函数`add`和`sub`。也可以在回调方法中直接使用表达式。例如：`count++`和`count--`。
