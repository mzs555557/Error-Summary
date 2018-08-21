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