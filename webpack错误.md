####webpack的使用问题####

关于{ <br>
	`>`Error: Cannot find module 'webpack-cli'
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:581:15)
    at Function.Module._load (internal/modules/cjs/loader.js:507:25)
    at Module.require (internal/modules/cjs/loader.js:637:17)
    at require (internal/modules/cjs/helpers.js:20:18)
    at runCommand.then (C:\Users\Administrator\AppData\Roaming\npm\node_modules\webpack\bin\webpack.js:152:5)
    at process._tickCallback (internal/process/next_tick.js:68:7) code: 'MODULE_NOT_FOUND' }的问题`<`<br>
#####首先:<br>
`npm uninstall --save-dev`卸载与webpack相关的所有依赖的名称,包括自己<br>
#####然后:<br>
`npm uninstall -g webpack webpack-cli`进行全局卸载<br>
#####再次设置:<br>
`npm install -g webpack webpack-cli`
#####之后<br>
`webpack--help`进行检测
#####最后<br>
`npm install --save-dev`安装在项目中