###classList新增方法
classList.add("")|添加多个类名
---|---
.remove()|移除
.length | 长度
.toggle("name")|有删除 ,无添加
.contains| 判断是否存在 true`/`false

###dataSet
ele.dataset|返回含data-XXX的数据
---|---
ele.dataset['aBcD'] ='1'|data-a-bc-d = "1"
delete ele.dataset['a'] | 删除 data-a
####atob-btoa<br>

atob|解析成我们能够识别的数据
--|--
btoa| 编译成计算识别的编码


####Proxy()
```
let p = new Proxy(target , handler);

```
####Object.create();创建object
#### 后台接收参数 @RequestParam ajax的data类型 json<br>后台接受参数 @@RequestBody ajax的data类型 String

####原型链

![原型链](./images/Prototype.png)



####const在es5中的使用
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

#####memary cache内存中的缓存 && disk cache 硬盘的缓存


####Class 继承示例

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


###Symbol()的使用
- ####每个Symbol值都是唯一的,因此该值不与其他任何值相等
 
```
let symbol1 = Symbol();
let symbol2 = Symbol();

console.log( symbol1 === symbol2); 
>false
```
- ####Symbol值不能与其它类型的值进行运算,会报错,Symbol可以显式转为字符串,也可以转为布尔值

```
let sym = Symbol('My symbol');

"your symbol is " + sym
//TypeError: can't convert symbol to string
`your symbol is ${sym}`
//TypeError: can't convert symbol to string
```
###作为属性名的symbol

- ####由于每个symbol的值都不相等,意味着Symbol值可以作为标识符

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

