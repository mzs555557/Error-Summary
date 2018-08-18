webpack的初级使用
---
####1.建文件:<br>
在根目录下建立src文件夹,新建名为app的js文件(执行文件)
####2.建webpack.config.js:<br>
导入以下文件:<br>

    const path = require('path');
    
    module.exports = {
      mode:"development",//开发环境 produnction//生产环境
      entry: './src/app.js',
      output: {
      path: path.resolve(__dirname, 'dist'),/*会生成dist文件夹*/
      filename: 'app.bundle.js'
      }
    };
<br>
####3.运行:<br>
`node dist/app.bundle.js`根目录下运行,输出src/app.js中的运行内容<br>
`webpack -p`生产环境<br>
`webpack -d`开发环境<br>
####4.插件配置:<br>
#####4.1.html-webpack-plugin<br>
`npm i -D html-webpack-plugin`下载插件<br>
在webpack.config.js中进行配置<br>
`const htmlWebpackPlugin = require('html-webpack-plugin');`<br>
在模块中:<br>

	module.exports = {
	    mode:"development",
	    entry: './src/app.js',
	    output: {
	        path: path.resolve(__dirname, 'dist'),
	        filename: 'app.bundle.js'
	    },
	    plugins: [
	        new htmlWebpackPlugin({
	            title:'自定义title',
	            filename : 'goudan/idx.html',//创建文件
	            template : './src/Tem.html'
	            /*
	            minify: {
	                collapseWhitespace: false //是否为压缩模式
	            }
	            */
	        }),
	    ]
	};
#####4.2.css与scss的使用:<br>
先`npm  -D sass-loader node-sass`<br>在`module.exports`中<br>
	
	module.exports = {
	  module: {
	    rules: [
	      {
	        test: /\.scss$/,
	        use: ExtractTextPlugin.extract({
	          fallback: 'style-loader',
	          use: ['css-loader', 'sass-loader']
	        })
	      }
	    ]
	  },
	  plugins: [
	    new ExtractTextPlugin('style.css')
	    //if you want to pass in options, you can do so:
	    //new ExtractTextPlugin({
	    //  filename: 'style.css'
	    //})
	  ]
	}
在app.js中引用css

#####4.3.es6转es5<br>
根目录创建.babelrc文件内容<br>

	{
	  "presets": ["es2015"],
	  "plugins": []
	}

---

`npm install babel-core babel-loader babel-preset-es2015 --save-dev`在module的rules中导入<br>

			{
                test: /\.js$/,
                use: 'babel-loader',
                exclude: /node_modules/
            }
之后创建es6语法规范的文件,在app.js中引用<br>
`import {fn} from './es5.js';`即可把文件转为es5格式