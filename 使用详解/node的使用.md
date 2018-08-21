node的使用:<br>
=============


npm init | 初始化项目环境
----     |  -----
npm init -y | 一路生成
npm install | 安装模块
npm i -g | 全局安装
npm i -save | 生产环境使用
npm i --save-dev | 开发环境使用
npm publish | 上传包名
npm unpublish -f | 卸载包名
npm login | 登录

###模块的导入<br>

	const koa = require("koa");
	const app = new koa();
	app.use(async (ctx) =>{
		ctx.body = "后台返回数据";	
	})
	app.listen(3000)

####1.1events:<br>

#####引用有以下两种方法:<br>
	const EventEmitter = require('events');
	class MyEmitter extends EventEmitter {}
	const myEmitter = new MyEmitter();

* * * 

	const EventEmitter = require('events');
	const myEmitter = new EventEmitter;

####使用:<br>
#####ES5:<br>

	myEmitter.on('event', function(a, b) {
	  console.log(a, b, this);
	  // 打印:
	  //   a b MyEmitter {
	  //     domain: null,
	  //     _events: { event: [Function] },
	  //     _eventsCount: 1,
	  //     _maxListeners: undefined }
	});
	myEmitter.emit('event', 'a', 'b');

#####ES6:<br>

	const myEmitter = new MyEmitter();
	myEmitter.on('event', (a, b) => {
	  console.log(a, b, this);
	  // 打印: a b {}
	});
	myEmitter.emit('event', 'a', 'b');

区别在于this的指向,ES5指向EventEmitter实例,ES6不再指向实例

####事件处理:<br>

`eventEmitter.on()`每次触发命名事件时调用<br>
`eventEmitter.once()`可以注册一个对于特定事件最多被调用一次的监听器。 当事件被触发时，监听器会被注销，然后再调用<br>
`eventEmitter.off()`解绑命名事件<br>
`emitter.eventNames()`返回一个列出触发器已注册监听器的事件的数组。 数组中的值为字符串或符号。<br>
`emitter.getMaxListeners()`返回 EventEmitter 当前的最大监听器限制值，该值可以通过 `emitter.setMaxListeners(n)` 设置或默认为 `EventEmitter.defaultMaxListeners`<br>
`emitter.listenerCount(eventName)`返回正在监听名为 eventName 的事件的监听器的数量<br>
`emitter.listeners(eventName)`返回名为 eventName 的事件的监听器数组的副本<br>
`emitter.removeAllListeners([eventName])`移除全部或指定 eventName 的监听器。<br>
`emitter.removeListener(eventName, listener)`从名为 eventName 的事件的监听器数组中移除指定的 listener。<br>

####path的使用:<br>

引用`const path = require('path');`<br>

`path.resolve([...paths])`会把一个路径或路径片段的序列解析为一个绝对路径。给定的路径的序列是从右往左被处理的<br>
`path.parse()`方法返回一个对象，对象的属性表示 path 的元素

	path.parse('/home/user/dir/file.txt');
	// 返回:
	// { root: '/',
	//   dir: '/home/user/dir',
	//   base: 'file.txt',
	//   ext: '.txt',
	//   name: 'file' }
