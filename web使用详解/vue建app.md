Vue:
===
从官网上引入vue文件.
vue指令

```js
v-text
v-html
v-show
v-if
v-else
v-else-if
v-for//与for使用相同
v-on
v-bind
v-model
v-pre
v-cloak
v-once
```
####使用实例:<br>
	<body>
	<div id="app">
	    <!--//数据插入到app作用域下需要用{{变量}}-->
	    {{ abc123 }}
	    <h2 v-text="vText"></h2>
	    <!--引入方式-->
	    <hr>
	    <div>
	        <ul>
	            <li v-for="item in arr">{{item}}</li>
	        </ul>
	    </div>
	</div>
	<script src="../js/vue.js">
	</script>
	<script>
	    // mvvm框架
	    new Vue({
	        el: '#app',
	        data: {//请求的原始数据,都会放到data中
	            abc123: 'hello World',
	            vText: '指令变量',
	            arr: [123,456,789]
	        }
	    });
	</script>

#####v-text:<br>
获取data中的内容
#####v-for:<br>
循环数组,获取其中内容:<br>
```js
		<ul>
            <li v-for="(key , index) in arr" :key="index">{{key}}</li>
        </ul>
        <hr>
        <ul>
            <li v-for="item in sortArr">{{item}}</li>
        </ul>
        <hr>
        <ul>
            <li v-for="(item , index) in users" :key="index">name:{{item.name}} age:{{item.age}}</li>
        </ul>
        <hr>
        <ul>
            <li v-for="(value , key , index) in userName">{{value}} {{key}} {{index}}</li>
        </ul>
```
#####v-on: <br>
用于事件监听,可以用@替代<br>

	<button @click="addition">加分</button>//触发addition函数
    <button @click="substration">减分</button>
    <hr>
    <button @keyup="onEnter">键盘</button>

#####v-model:<br>
数据的双向绑定:<br>

```js
<h1>{{num}}</h1>
<label>
  <input type="text" v-model="num" @keyup.enter="onEnter" value="键盘事件">
</label>

```
两组num数据会相互影响 ,数据的影响是双向的