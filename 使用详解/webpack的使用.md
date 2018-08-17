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