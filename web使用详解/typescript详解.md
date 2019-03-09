####typescript的数据类型
```
const value:string|array|number|... //使用前先定义变量的数据类型

枚举类型
enum msg {one = 1 , two = 2}
let c:msg = msg.one;
console.log(c)// 输出1

//任意类型
var num:any // 任意数据类型
//函数的类型
function run():number {返回number数据类型
}

//数组的定义方法
var arr1:number[] = [11,22,33];
var arr2:Array<number> =[11,22,33]
var arr3:any[] = ['1231312' , 22 ,55]

//关于函数的定义
function msg(name:string , age:number , like?:string//可选参数):string {

}

//方法的重载
function code(name:string):string;
function code(name:string ,age:number):string;
function code(name:any , age?:any):any{
	if(age){
		console.log('我叫'+name + 'age' + age);
	}else{
		console.log('我叫' + name);
	}
}

```

####typescript中的类
```
---es5中构造方法与类
function Person(){
	this.name = "";
	this.age = 1;
	this.run = function(){}
}
Person.prototype.work = function(){}//动态方法
Person.getInfo = function(){}//静态方法

var p = new Person();
p.work();;
p.run();
Person.getInfo();//调用静态方法

----es5的继承
function Web(){
	Peron.call(this);
}
可以继承构造的方法
但不能继承原型链的方法
var w = new Web();
w.run()//可以运行
w.work()//不能运行

Web.prototype = new Person(); //继承原型链的方法和构造函数的方法 //但无法传参

----组合方法
function Web(){
	Peron.call(this);
}
Web.prototype = new Person();



---typescript的类与继承

Class Person{
	name:string;
	constructor(name:string){
		this.name = name;
	}
	getName(){
		return this.name;
	}
	setName(name:string):void{
		this.name = name;	
	}
}

var p = new Person('lisi');
p.getName()//lisi
p.setName('vhsj');
p.getName();//vhsj

Class Web extends Person{
	constructor(name:string){
		super(name);
	}
}
var w = new Web('123');

//类的三种修饰符 public protected private
```
