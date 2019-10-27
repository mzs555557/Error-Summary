### classList新增方法

classList.add("")|添加多个类名
---|---
.remove()|移除
.length | 长度
.toggle("name")|有删除 ,无添加
.contains| 判断是否存在 true`/`false

### dataSet
ele.dataset|返回含data-XXX的数据
---|---
ele.dataset['aBcD'] ='1'|data-a-bc-d = "1"
delete ele.dataset['a'] | 删除 data-a
#### atob-btoa<br>

atob|解析成我们能够识别的数据
--|--
btoa| 编译成计算识别的编码

#### 防抖与节流

```
 window.onload = function(){
            var myDebounce = document.getElementById("debounce");
            var myThrottle = document.getElementById("throttle");
            myDebounce.addEventListener("click" ,  debounce(sayDebounce));
            myThrottle.addEventListener("click" , throttle(sayThrottle));
        }
        //防抖功能的函数
        function debounce(fn){
            let timeout = null;
            return function(){
                clearTimeout(timeout);

                timeout = setTimeout(()=>{
                    fn.call(this , arguments);
                } , 1000);
            }
        }
        function sayDebounce(){
            console.log("防抖成功!!");
        }
        ///节流功能的函数
        function throttle(fn) {
            let canRun = true;
            return function(){
                if(!canRun){
                    return;
                }
                canRun = false;
                setTimeout(()=>{
                    fn.call(this , arguments);
                    canRun = true;
                } , 1000)
            }
        }
        function sayThrottle(){
            console.log("节流成功");
        }

```
####重绘与回流
```

```
#### Proxy()

```
let p = new Proxy(target , handler);
```
#### Object.create();创建object

#### 后台接收参数 @RequestParam ajax的data类型 json<br>后台接受参数 @@RequestBody ajax的data类型 String

#### 原型链

![原型链](./images/Prototype.png)



#### const在es5中的使用

```js
	var _const = function _const(data , value){
        window.data = value;
        Object.defineProperty(window, data , {
            enumrable:false,
            configurable:false,
            get:function(){
                return value;
            },
            set:function(){
                if (data !== value) {
                    // statement
                    throw  new TypeError('Assignment to constant variable.')
                } else {
                    // statement
                    return value;
                }
            }
        })
       }
```

##### memary cache内存中的缓存 && disk cache 硬盘的缓存

#### Class 继承示例

```
//bad 
function Queue(contents = []){
	this._queue = [...contents];
}
Queue.prototype.pop = function() {
	const value = this._queue[0];
	this._queue.splice(0 , 1);
	return value;
}
// good

class Queue {
	constructor(contents = []) {
		this._queue = [...contents];
	}
	pop() {
        const value = this._queue[0];
		this._queue.splice(0 , 1)
		return value;
    }
}

//使用extends实现继承,不会有破坏 instanceof 运算的危险

//bad
const inherits = require('inherits');
function PeekableQueue(contents) {
	Queue.apply(this , contents);
}
inherits(PeekableQueue , Queue);
PeekableQueue.prototype.peek = function() {
	return this.queue[0];
}
//good
class PeekableQueue extends Queue {
	peek() {
		return this._queue[0];
	}
}
 
```


### Symbol()的使用
- #### 每个Symbol值都是唯一的,因此该值不与其他任何值相等

```
let symbol1 = Symbol();
let symbol2 = Symbol();

console.log( symbol1 === symbol2); 
>false
```
- #### Symbol值不能与其它类型的值进行运算,会报错,Symbol可以显式转为字符串,也可以转为布尔值

```
let sym = Symbol('My symbol');

"your symbol is " + sym
//TypeError: can't convert symbol to string
`your symbol is ${sym}`
//TypeError: can't convert symbol to string
```
### 作为属性名的symbol

- #### 由于每个symbol的值都不相等,意味着Symbol值可以作为标识符

```
let mySymbol = Symbol();

//first write methods
let a = {};
a[mySymbol] = 'Hello!';
//second
let a = {
    [mySymbol]: 'Hello!'
};
//third
let a = {};
Object.definProperty(a , mySymbol, { value: 'Hello'});

// 以上写法的结果相同
a[mySymbol] //"Hello!"
```
### Symbol属性名的遍历

```
Symbol作为属性名,不会出现在for .. in , for ... of 循环中, 也不会被Object.keys() , Object.getOwnPropertyNames() , JSON.stringify()返回
但Object.getOwnPropertySymbols(obj);方法返回一个数组,成员是当前对象的所有用作属性名的Symbol值
----
const obj = {};
let a = Symbol('a');
let b = Symbol('b');

obj[a] = 'Hello';
obj[b] = 'World';

const objectSymbols = Object.getOwnPropertySymbols(obj);

objectSymbols//[Symbol(a) , Symbol(b)]
---- Reflect.ownKeys方法可以返回所有类型的键名 包括常规键名 与 Symbol键名 
let obj = {
	[Symbol('my_key')]:1,
	enum:2,
	nonEnum:3
}

Reflect.ownKeys(obj);
----由于以Symbol值作为名称的属性不会被常规方法遍历得到,可以为对象定义一些非私有的,用于内部的方法

let size = Symbol('size');

class Collection{
	constructor(){
		this[size] = 0;
	}
	add(item){
		this[this[size]] = item;
		this[size] ++;
	}
	static sizeof(instance) {
		return instance[size]
	} 
}
let x = new Collection();
Collection.sizeof(x)

x.add('foo');
Collection.sizeOf(x);

Object.keys(x) // ['0']
Object.getOwnPropertyNames(x)//['0']
Objec.getOwnPropertySymbols(x) // [Symbol(size)]

```
###Symbol.for() , Symbol.keyFor()
```
Symbol.for() 与 Symbol() 都会生成新的 Symbol 前者会被登记在全局供搜索,后者不会
----
Symbol.for("bar") === Symbol.for("bar")
// true

Symbol("bar") === Symbol("bar")
// false
----
Symbol.keyFor方法返回一个已登记的Symbol类型值的key
----
let s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

let s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined

```

###模块的Singleton模式
- Singleton 模式指的是调用一个类,任何时候返回同一实例

```
function A(){
  this.foo = 'hello';
}

if(!global._foo){
  global._foo = new A();
}
module.exports = global._foo;
```
- 引入上面的代码时 , a任何时候加载都是A的同一个实例, 但是全局变量global._foo 是可以改写的,任何文件都可以修改

```
global._foo = {foo : 'world'}; // 修改了变量
const a = require('./mod.js');
console.log(a.foo);
```
- 可以保证 global[FOO_KEY]不会被无意间覆盖 , 但仍可改写

```
const FOO_KEY = Symbol.for('foo');

function A() {
  this.foo = 'hello';
}

if(!global[FOO_KEY]) {
  global[FOO_KEY] = new A();
}

module.exports = global[FOO_KEY];
```

```
global[Symbol.for('foo')] = {foo :'world !'};

```

- 如果键名使用Symbol方法生成 , 那么外部将无法引用这个值 , 也无法改写

```
const FOO_KEY = Symbol('foo');

```

###Proxy

```
用于修改某些操作的默认行为,等同于在语言层面作出修改,所以属于一种"元编程" , 即对编程语言进行编程
-------
var obj = new Proxy({}, {
  get: function(target, key, receiver) {
    console.log(`getting ${key}!`);
    return Reflect.get(target, key, receiver);
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return Reflect.set(target, key, value, receiver);
  }
});
上面的代码对一个空对象架设了一层拦截,重定义了属性的读取和设置行为
obj.count = 1;
//setting count
++obj.count
//getting count
//setting count

Proxy实际上重载了点运算符,即用自己的定义涵盖了语言的原始定义

var proxy = new Proxy(target,hanlder);
var proxy = new Proxy({}, {
  get: function(target , property) {
    return 35;
  }
});
proxy.time //35  proxy.name //35
上面的代码中作为构造函数, Proxy接受两个参数. 第一个参数是所要代理的目标对象,即如果没有 Proxy的介入 , 操作原来要访问的就是这个对象,第二个参数是配置对象,对于每一个被代理的操作,需要提供一个对应的处理函数,该函数将拦截对应的操作. 上述代码中,由于拦截函数总是返回35 , 所以任何属性都将得到35.
--------

var handler = {
	get: function(target, name) {
		if (name === 'prototype') {
			return Object.prototype;
		}
		return 'Hello, ' + name;
	},

	apply: function(target, thisBinding, args) {
		return args[0];
	},

	construct: function(target, args) {
		return { value: args[1] };
	}
};

var fproxy = new Proxy(function(x, y) {
	return x + y;
}, handler);

console.log(fproxy(1, 2));//1
console.log(new fproxy(1, 2));//{value:2}
console.log(fproxy.prototype === Object.prototype);//true
console.log(fproxy.foo === 'Hello, foo');//true

-------
```
- get(target , propKey, receiver) : 拦截对象属性的读取,比如 proxy.foo和proxy['foo']
- set(target , propKey , value ,receiver): 拦截对象属性的设置,比如 proxy.foo = v 或 proxy['foo'] = v 返回一个布尔值
- has(target , propKey) 拦截propKey in proxy 的操作,返回一个布尔值
- deleteProperty(target, propKey)：拦截delete proxy[propKey]的操作，返回一个布尔值。
- ownKeys(target)：拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性。
- getOwnPropertyDescriptor(target, propKey)：拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。
- defineProperty(target, propKey, propDesc)：拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。
- preventExtensions(target)：拦截Object.preventExtensions(proxy)，返回一个布尔值。
- getPrototypeOf(target)：拦截Object.getPrototypeOf(proxy)，返回一个对象。
- isExtensible(target)：拦截Object.isExtensible(proxy)，返回一个布尔值。
- setPrototypeOf(target, proto)：拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。
- apply(target, object, args)：拦截 Proxy 实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。
- construct(target, args)：拦截 Proxy 实例作为构造函数调用的操作，比如new proxy(...args)。


