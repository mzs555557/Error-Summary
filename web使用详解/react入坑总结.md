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
			this.context.router.history.push('/#');	//实现页面的跳转  注意this
		}
	}	
	

```
###jsx不能使用if else 判断 必须引用三元表达式
###react事件采取驼峰命名 内部可使用ES6的函数
###react表单数据的使用实例<br>
```js
	import React , {Component} from 'react';
	import { Input, Button, Grid, Feedback, Select } from '@icedesign/base';
	import {
	  FormBinderWrapper as IceFormBinderWrapper,
	  FormBinder as IceFormBinder,
	  FormError as IceFormError,
	} from '@icedesign/form-binder';

	export default class Register extends Component{
		constructor(props){
			super(props);;
			this.state = {
				value:{
					userSnum: '',
			        email: '',
			        passwd: '',
			        rePasswd: '',
			        class: '',
			        group: '',
				}
			}
		}
		
		reander(){
			return(
				<IceFormBinderWrapper
				  value={this.state.value}
				  onChange={this.formChange}	
				  ref="form"
				>
					
					<FormBinder
						name="userSnum"
						required
						message=""
					>
						<Input size="large" placeholder="学号">
					</FormBinder>

				</IceFormBinderWrapper>
				
			)

		}
		
	}

```
###react</br>
```js
	cnpm i react react-dom babel-standaload -S
	<script src=''></script>//引入文件
	window.Name = class Name extends ReactDom.component{
		render{
			return (
				
			)
		}
	}
```

###react中this与事件的绑定<br>
在class类中声明的函数调用时需要现在构造函数中声明
```js
	class App extends React.Component{
		constructor(){
			super();
			this.state ={ 
				data:name
			}
			this.click = this.click.bind(this)	
		}
		
		click(){
			
		}
	}
	render(){
		return(
			<div onClick={this.click}></div>
		)
	}

```
###react子类调用父类的方法<br>
再父类中声明的方法需要在父组件声明,子组件继承
```js
	class App extends React.Component{
		constructor(){
			super();
			this.state ={ 
				data:name
			}
			this.click = this.click.bind(this);
		}
		
		click(){
			console.log('1');
		}
	}
	render(){
		return(
			<child click={this.click}></child>
		)
	}
}


	class child extends React.Component{
		constructor(props){
		super(props);
		this.state = {
			click: props.click
		}

		render(){
			return(
				<div>
					<div onClick={this.state.click}></div>
				</div>	
			)
		}
	}
	
```
####函数中this.state.msg = 'xx'不会影响视图更新 this.setState({})影响视图更新


#####创建react脚手架`npm install -g create-react-app`   &nbsp; `create-react-app 名称`创建脚手架 `cd 名称` `npm start`运行

```js
	window.history.href = '#abc'
	window.history.pushState('')
```

#####组件内容限制
	import PropTypes from 'prop-types';
	组件名.propTypes ={
		data: propTypes.string,
		
	}

####router使用

在写列表跳转时不能与父路由重复,否则父路由也会跟着显示 (或者加exact严格匹配模式)

```js
	
	import {BrowserRouter as Router , Route , Link} from 'react-router-dom'
	
	class XX extends Component {
		render (){
			return (
				<Router>
					<div>
						 <h1>{this.state.title}</h1>
		                    <h2>
		                        <Link to='/'>首页</Link>
		                        <Link to='/news'>新闻</Link>
		                        <Link to='/shopList'>商品</Link>
		                    </h2>
		
		                    <br/>
		                    <br/>
		                    <hr/>
		                    <Route exact path='' component={Home}/>
		                    <Route path='/news' component={NewList}/>
		                    <Route path='/shopList' component={shopList}/>
							<Route path='/shopContent/:id' component={shopContent} />	
					</div>
				</Router>			
			)
		}
		
	}

	export default XX;
```

#####url
```js
	`cnpm i url -D`

	import Url from 'url';
	const query = Url.parse(this.props.location.search , true).query
	
```
####在create-react-app中引用组件需配置样式
#####使用`antd-mobile`组件时在package.json修改以下配置在可以引入样式
```js
	"babel":{
	++ "plugins":{
			["import", { libraryName: "antd-mobile", "style": "css" }]
        }	
	}	

```

####页面路由的控制
```js
<Router basename='router'>
            <Switch>
                <Route path='/' render ={()=>{
                  return (
                    <Switch>
                        {
                          routes.map((item , index) => {
                            if(item.exact) {
                              return (
                                <Route
                                    key={index}
                                    exact ={item.exact}
                                    path = {item.path}
                                    component = {item.component}                                
                                >
                                </Route>
                              )
                            }
                            return (
                              <Route
                                key = {index}
                                path = {item.path}
                                render= {()=>{
                                  return < item.component abc={'123'} />
                                }}>
                                </Route>
                            )
                          })
                        }
                    </Switch>
                  )
                }}>

                </Route>
            </Switch>
          </Router>
```


#####关于npm端口占用报错:
`netstat -aon|findstr
"3000"`

`taskkill /pid number -f`

###react首次创建至渲染页面
	constructor（）    构造函数，在创建组件的时候调用一次
	componentWillMount(){
		console.log("组件即将挂载")
	}
	componentDidMount(){
		console.log("组件已经挂载")
	}
	componentWillReceiveProps(nextProps){
		console.log("组件要接受父组件的值")		
	}
	shouldComponentUpdate(){
		console.log("判断是否要更新组件")
	}
	componentWillUpdate(){
		console.log("马上要更新组件了")
	}
	componentDidUpdate(){
		console.log("组件更新完毕")
	}
	componentWillUnmount(){
		console.log("组件卸载了")
	}

####关于redux的基本使用<br>
	
	import {createStore} from 'redux';
	    function counter(state = 0, action){
	      switch(action.type){
	        case '加机关枪':
	          return state + 1;
	        case '减机关枪':
	          return state - 1;
	        default:
	          return 10;
	      }
	    }
	    const store = createStore(counter);
	    const init = store.getState()
	
	    console.log(init);
	
	    function listener(){
	       const current = store.getState();
	       console.log(`现有机关枪${current}把`); 
	    }
	    store.subscribe(listener);
	    store.dispatch({type:'加机关枪'})
	    store.dispatch({type:'加机关枪'})
	    console.log(store.getState());
	    store.dispatch({type:'减机关枪'})


