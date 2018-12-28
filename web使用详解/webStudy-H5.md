###classList新增方法<br>
classList.add("")|添加多个类名
---|---
.remove()|移除
.length | 长度
.toggle("name")|有删除 ,无添加
.contains| 判断是否存在 true`/`false

###dataSet<br>
ele.dataset|返回含data-XXX的数据
---|---
ele.dataset['aBcD'] ='1'|data-a-bc-d = "1"
delete ele.dataset['a'] | 删除 data-a
####atob-btoa<br>
atob|解析成我们能够识别的数据
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