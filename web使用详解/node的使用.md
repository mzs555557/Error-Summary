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

####url与querystring的使用:<br>

	const {URL} = require('url');
	const myUrl = new URL('https://user:pass@sub.host.com:8080/p/a/t/h?query=string#hash');
	const qs = require('querystring');
	console.log(qs.parse(myUrl));

####crypto加密:<br>

	const crypto = require('crypto');
	
	const script = 'abcdefg';
	const hash = crypto.createHmac('md5' , secret).update("asd").digest("hex");

####fs数据:<br>
const fs = require('fs');

	fs.unlink('/tmp/hello', (err) => {
	  if (err) throw err;
	  console.log('成功删除 /tmp/hello');
	});
	fs.rename('/tmp/hello', '/tmp/world', (err) => {
	  if (err) throw err;
	  console.log('重命名完成');
	});
	fs.stat('/tmp/world', (err, stats) => {
	  if (err) throw err;
	  console.log(`文件属性: ${JSON.stringify(stats)}`);
	});

	fs.open('myfile', 'wx', (err, fd) => {
	  if (err) {
	    if (err.code === 'EEXIST') {
	      console.error('myfile already exists');
	      return;
	    }
	
	    throw err;
	  }
	
	  writeMyData(fd);
	});

####简单爬虫的设计:<br>

	const http = require('https');
	const koa = require('koa');
	const app = new koa;
	app.use(async ctx => {
	    let arr = [];
	    let biliurl = 'https://bangumi.bilibili.com/media/web_api/search/result?season_version=-1&area=-1&is_finish=-1&copyright=-1&season_status=-1&season_month=-1&pub_date=-1&style_id=-1&order=3&st=1&sort=0&page=1&season_type=1&pagesize=20';
	    await new Promise(resolve => {
	        http.get(biliurl, res => {
	        let data = '';
	        res.on('data', chunk => {
	            data += chunk;
	        });
	        res.on('end',  async function () {
	                let json = JSON.parse(data);
	                arr = json.result.data;
	                console.log(1);
	                resolve(arr);
	            });
	        }).on('error', () => {
	            console.log('获取数据错误');
	        });
	    });
	    console.log(2);
	    ctx.body = arr;
	});
	app.listen(3000);

<hr>	

	const koa = require('koa');
	const cheerio = require('cheerio');
	const request = require('superagent');
	const {join} = require('path');
	const app = new koa;
	app.use(async ctx => {
	    let arr = [];
	    for (let num = 1; num < 20; num++) {
	
	        await new Promise(resolve => {
	            request
	                .get(`https://book.douban.com/tag/%E5%A5%87%E5%B9%BB?start=${num * 20}`)//https://www.bilibili.com/v/douga/
	                .end((err, res) => {
	                    const data = res.text;
	                    const $ = cheerio.load(data);
	                    $('#subject_list > .subject-list > .subject-item').each((i, v) => {
	                        let $v = $(v);
	                        let obj = {
	                            author: $v.find('.info > h2 > a').prop('title').trim(),
	                            Introduce: $v.find('.info > p').text().trim(),
	                            evaluation: $v.find('.rating_nums').text().trim(),
	                            url: $v.find('.pic > .nbg').prop('href').trim()
	                        };
	                        arr.push(obj);
	                        console.log(num);
	                        resolve(JSON.stringify(arr));
	                    })
	                });
	        });
	    }
	    ctx.body = arr;
	});
	
	app.listen(3003);

####mongoose的使用:<br>

	const mongoose = require('mongoose');
	
	const db = mongoose.createConnection('mongodb://localhost:27017/fengyu', {useNewUrlParser: true});
	//用原生es6的promise取代mongoose自实现的promise
	mongoose.promise = global.promise;
	//操作之前,使用Schema设置字段的数据类型
	db.on("error", console.log.bind(console, "数据库连接失败"));
	db.on("open", () => {
	    console.log('数据库连接成功');
	});
	//连接成功 , 操作数据库
	const Schema = mongoose.Schema;
	
	const JsSchema = new Schema({
	    name: String,
	    age: Number,
	    sex: {
	        type: String,
	        default: '男'
	    }
	}, {
	    versionKey: false,
	});
	const Js = db.model("javascript", JsSchema);//建立collections
	const data = {
	    name: "dashuaibi",
	    age: 30,
	};
	const data2 = {
	    name: '小清新',
	    age: 19,
	    sex: '女'
	};
	const d1 = new Js(data2);//插入数据
	d1.save().then(res=>{
	    console.log(res);
	}).catch(error=>{
	    console.log(error);
	});

####利用nodejs建立博客管理系统:

模板 | pug
--   | --
数据库 | MongoDB
 后台 | nodejs
模仿 | layui界面

