###react路由跳转
```js
	import React  , {Component} from "react";
	import ProTypes from "prop-types"

	class MyComponent extends Component{
		static contextTypes = {
			router:PropTypes.object
		}
		constructor(props , context){
			super(props , context);
			
		}
		MyFunction(){
			this.context.router.history.push('/#');	//实现页面的跳转
		}
	}	
	

```
###jsx不能使用if else 判断 必须引用三元表达式