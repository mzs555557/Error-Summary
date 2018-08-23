语法<br>
===

####1.1:<br>
`obj.replace(/^\s+|\s+$/g , "")`与trim()方法相同<br>

####1.2.1建库的首要基本套路<br>

	(function(window,document,undefine){
		let Fy = function(str) {
			return new Fy.prototype.init(str)
		}		
		Fy.prototype = {
			constructor: Fy,
			init: function(select){
				

			}

		}

		Fy.prototype.init.prototype = Fy.prototype;
		window._fy = Fy;
	})(window,document)

####1.2.2选择器的正则表达:<br>

选择器 | 表达式
---- | ---
id | /^#/.test(obj)
类选择器 |  /^\./
插入元素	| /^</
css3 | /^[~+>\s]/
标签选择器| /^[\w]/

	let reg = /^[a-z]{5,17}$/ig;//正则表达全局匹配成功时会记录匹配下标
	let str1 = "asdasdsadadasd";
	let str2 = "asdasdsfsgfgdf";
	let str3 = "asdsdghfghfggj";
	let str4 = "ddslkjdlsfdlkjg";
	
	console.log(reg.test(str1))//true
	//匹配成功,记录lastIndex 
	console.log(reg.test(str1))//false
	//匹配失败,重置lastIndex = 0;
	console.log(reg.test(str1))//true
	console.log(reg.test(str1))//flase
	//去除/g之后则全部为true

####1.2.3window.scrollBy<br>

在窗口中按指定的偏移量滚动文档<br>

###1.3 兼容性<br>
####1.3.1关于getElementByClassName的兼容写法:<br>

	if(!document.getElementsByClassByName){
		document.getElementsByClassName = function(eleName){
			let ele = document.getElementsByTagName("*"),
				eleAry = [],
				reg = new RegExp('\\b'+ eleName + '\\b');	
			for(let i = 0;i < ele.length;i++){
				if(reg.test(ele[i].className)) {
					eleAry.push(ele[i]);
				}
			}
		}
		return eleAry;
	}
		
####1.3.2关于querySelectorAll的兼容性写法:<br>

	if(!document.querySelectorAll) {
		document.querySelectorAll = function (str) {
            let style = document.createElement('style'),
                elements = [],
                element = null;
            document._fy = [];
            //head标签
            let head = document.documentElement.firstChild;
            head.appendChild(style);
            style.styleSheet.cssText = str + "{fy: expression(document.__fy && document.__fy.push(this))}"
            window.scrollBy(0,0);
            style.parentNode.removeChild(style);
            while(document._fy.length) {
                element = document._fy.shift();
                element.style.removeAttribute("fy");
                elements.push(element);
            }
            document._fy = null;
            return elements;
        }
	}	

####1.3.3数组方法:<br>

类数组转数组:<br>

	function array(0){
		return [].slice.call(o)
	}

<br>
`foreach`方法<br>

	function each(arr , fn , that){
		for( let i = 0; i < arr.length; i++ ){
			let flag = fn.call(that || arr[i] , arr[i] , i , arr)
			if(flag === false) {
				break;		
			} else if (flag === false) {
				continue;
			}
		} 
	}


`arr.shift()`删除并返回数组的第一个元素<br>

###1.4内部方法:<br>

#####1.4.1用于处理事件修饰符/事件指令<br>

	let _eventModifiers = function (arr , e) {
		arr.foreach((v)=>{
			if(v === "stop") {
				if(e.stopPropagation){
					e.stopPropagation();
				}else{
					e.cancelBubble = true;
				}		
			} else if (v === "prevent") {
				if(e.preventDefault) {
					e.preventDefault();
				}else{
					e.returnValue = false;
				}
			}	
		})
	}

#####1.4.2内部方法,用于储存事件函数

	let _addEventFn = function(obj){
		if(typeof obj.dom.events === "undefined") {
			obj.dom.events = {};
			obj.dom.events[obj.type] = [obj.fn];
		}else if(obj.dom.events[obj.type] instanceof Array) {
			obj.dom.events[obj.type].push(obj.fn);
		}else {
			obj.dom.events[obj.type] = [obj.fn];
		}
		obj.dom.events[obj.type].origin = obj.origin;
	}