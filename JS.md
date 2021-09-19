#  JS

### 1.js中的charCodeat方法

```javascript
var str1 = 'abc'
console.log(str1.charCodeat(1)) // b -> 101
// 接受的参数是该字符串的第几个位置 这里示例1就是b这个
// 函数返回的就是该字符的 Unicode编码
```

### 2.split注意

```js
var str1 = "aaaaa"
console(str1.split('.'))  // ["aaaaa"]
// 如果你选择切割的字符 在你str1中没有的 那么它会将原来的串 放到一个数组中返回给你
```

### 3.apply

```js
fun.apply(thisArg, [param1,param2,...])
/*
	1.thisArg:
		1.fun的this指向thisArg对象
         2.非严格模式下：thisArg指定为null，undefined，fun中的this指向window对象.
         3.严格模式下：fun的this为undefined
         4.值为原始值(数字，字符串，布尔值)的this会指向该原始值的自动包装对象，如 String、Number、Boolean
    2.param1,param2:
     	1.如果param不传或为 null/undefined，则表示不需要传入任何参数.
	    2.apply第二个参数为数组，数组内的值为传给fun的参数。
	3.如何不弄混这个apply和call
	    1.apply是以a开头，它传给fun的参数是Array，也是以a开头的。
调用apply的必须是一个函数
	4.bind / call与apply 的区别：
		1.call/apply改变了函数的this上下文后马上执行该函数
		2.bind则是返回改变了上下文后的函数,不执行该函数
		3.call/apply 返回fun的执行结果
		4.bind返回fun的拷贝，并指定了fun的this指向，保存了fun的参数。
*/
// 1.常用判断类型
function isType(data, type) {
   const typeObj = {
      '[object String]': 'string',
      '[object Number]': 'number',
      '[object Boolean]': 'boolean',
      '[object Null]': 'null',
      '[object Undefined]': 'undefined',
      '[object Object]': 'object',
      '[object Array]': 'array',
      '[object Function]': 'function',
      '[object Date]': 'date', // Object.prototype.toString.call(new Date())
      '[object RegExp]': 'regExp',
      '[object Map]': 'map',
      '[object Set]': 'set',
      '[object HTMLDivElement]': 'dom', // document.querySelector('#app')
      '[object WeakMap]': 'weakMap',
      '[object Window]': 'window',  // Object.prototype.toString.call(window)
      '[object Error]': 'error', // new Error('1')
      '[object Arguments]': 'arguments',
   }
   let name = Object.prototype.toString.call(data) // 借用Object.prototype.toString()获取数据类型
   let typeName = typeObj[name] || '未知类型' // 匹配数据类型
   return typeName === type // 判断该数据类型是否为传入的类型
}
console.log(
        isType({}, 'object'), // true
        isType([], 'array'), // true
        isType(new Date(), 'object'), // false
        isType(new Date(), 'date'), // true
)
// 常用2 往类数组中添加元素 借用Array的方法push
var arrayLike = {
   0: 'OB',
   1: 'Koro1',
   length: 2
}
Array.prototype.push.call(arrayLike, '添加元素1', '添加元素2');
console.log(arrayLike) // {"0":"OB","1":"Koro1","2":"添加元素1","3":"添加元素2","length":4}

// 常用3 一个数组中的最大值 Math.max方法接收数组是不管用的只能这么接收 Math.max(1,2,3)
let arra1 = [1,19,0,20,22]
const amax = Math.max.apply(Math,arra1)
console.log(amax)

// call 与 apply 用哪个？
/*
	参数数量/顺序确定就用call，参数数量/顺序不确定的话就用apply。
	考虑可读性：参数数量不多就用call，参数数量比较多的话，把参数整合成数组，使用apply。
	参数集合已经是一个数组的情况，用apply，比如上文的获取数组最大值/最小值。
*/
```

### 4.then()的使用

```js
// then()方法是异步执行
// 当then()之前的方法执行完毕之后才会执行后面的方法 保证数据能取到
```

### 5.正则中的test方法

```js
var part1 = RegExp('a')
var str1 = 'aabb'
var result = part1.test(str1) // 是否匹配正则
// 匹配result为true 否则false
```

### 6.throttle-debounce

```js
// 防抖和节流的函数库
import { throttle, debounce } from 'throttle-debounce';
function foo() { console.log('foo..'); }
function bar() { console.log('bar..'); }
const fooWrapper = throttle(200, foo);
for (let i = 1; i < 10; i++) {
  setTimeout(fooWrapper, i * 30);
}
// => foo 执行了三次
// => foo..
// => foo..
// => foo..
const barWrapper = debounce(200, bar);
for (let i = 1; i < 10; i++) {
  setTimeout(barWrapper, i * 30);
}
// => bar 执行了一次 
// => bar.
10.129.130.251:8080
http://10.129.130.251/efrd/technic/fcp-ui-preview/fcp-ui-modules.git
http://10.129.130.251:8080/efrd/technic/fcp-frontend-base.git
```

### 7.查看npm目录

```
npm config list
```

### 8.assign

```js
// 合并对象 将sources中的枚举属性和值复制到target 如果target如果已经有这个属性了则会覆盖它
Object.assign(target,…sources)
// tagget 改变哪个对象  ...source改变成什么样子
var a1 = {a:1}
var a2 = {b:2}
var a3 = {c:3}

var obj = Object.assign({},a1,a2,a3)
console.log(obj) // {a:1,b:2,c:3}
```

### 9.vue中的foreach

```js
data:{
	numList:[1,2,3,4,5]
}
methods:{
	exchangeArray(){
		this.numList.foreach(num=>{
			console.log(num+10)
		})
	}
}
// 打印 11 12 13 14 15
```

### 10.some方法

```js
var array = [1, 2, 3, 4, 5];
var even = function(item, index, array) {
  return item% 2 === 0;
};
console.log(array.some(even)); //true


// 只要數組中有一個滿足條件 那麽就會返回true
```

### 11.js中執行順序

```js
setTimeout(function() {
    console.log('我是定时器！');
})
new Promise(function(resolve) {
    console.log('我是promise！');
    resolve();
}).then(function() {
    console.log('我是then！');
})
console.log('我是主线程！');

执行顺序：
我是promise！
我是主线程！
我是then！
我是定时器！

// 宏任務与微任务与主线程
// seTimeOut为一个宏任务 放到宏任务队列中 Promise是主线程任务 then则是微任务 console.log()是主线程的任务 所以线执行主线程的任务 promise 和 console.log(我是主线程) 然后微任务是比宏任务优先级高的 所以执行微任务 最后再执行宏任务
```

### 12.Object(未完成)

```js
// Object.create()
const person = {
  isHuman: false,
  printIntroduction: function() {
    console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
  }
};
// 先搞一个person对象

const me = Object.create(person);

me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
me.isHuman = true; // inherited properties can be overwritten

me.printIntroduction();
// expected output: "My name is Matthew. Am I human? true"
// Object.create()看这吧 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create



// Object.keys()
// 简单使用
// simple array
var arr = ['a', 'b', 'c'];
console.log(Object.keys(arr)); // console: ['0', '1', '2']

// array like object
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.keys(obj)); // console: ['0', '1', '2']

// array like object with random key ordering
var anObj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.keys(anObj)); // console: ['2', '7', '100']

// getFoo is a property which isn't enumerable
var myObj = Object.create({}, {
  getFoo: {
    value: function () { return this.foo; }
  }
});
myObj.foo = 1;
console.log(Object.keys(myObj)); // console: ['foo']


// Objec.defineProperty
var obj = {}, value = null;
Object.defineProperty(obj, "num", {
    get: function(){
        console.log('执行了 get 操作')
        return value;
    },
    set: function(newValue) {
        console.log('执行了 set 操作')
        value = newValue;
    }
})

obj.num = 1 // 执行了 set 操作

console.log(obj.num); // 执行了 get 操作 // 1

  function ArrayLi() {
    this.value = null
    var arr = []
    Object.defineProperty(this,'num',{
      get(){
        console.log('执行get啦')
        return value
      },
      set(value){
        console.log('执行set啦')
        this.value = value
        console.log(this.value)
        arr.push({val:value})
      }
    })
    this.getarr = function () {
     return arr
    }
  }
  var arr1 = new ArrayLi()
  arr1.num = 1 // 执行set啦
  console.log(arr1.getarr()) // {val:1}
  console.log(arr1.value) // set 操作中将value设置为了1

// Object.defineProperty  结束

// Objec.defineProperties
var obj = {
    name:'lbj',
    age:18,
}

Object.defineProperties(obj,{
    name:{value:'kobe',writable:false} 
    // 当writable 未true则允许修改 为false时不允许修改
    // value就是你要修改成什么值
})
console.log(obj)

// Object.getOwnPropertyDescriptor()
var obj = {
    name:'lbj',
    age:18,
}
console.log(Object.getOwnPropertyDescriptor(obj,'name')) // 注意第二个值是属性值 必须是字符串形式
// 打印结果不仅可以获取值 并且可以获取它的配置 比如是否可以修改 就是上面的那些 writable 那种配置

// Object.getOwnPropertyNames()
var obj = {
    name:'lbj',
    age:18,
}
console.log(Object.getOwnPropertyNames(obj))
// 打印 ['name','age']

// Object.preventExtensions
var obj = {
    name:'lbj',
    age:18,
}
Object.preventExtensions(obj) // 当你设置了这个 下面你再为对象添加属性 也不管用了
obj.newname = '你号啊 我是一个信纸'
console.log(obj)

// Object.freeze()
var obj = {
    name:'lbj',
    age:18,
}
Object.freeze(obj) // 设置之后 任何操作都不能改变对象
obj.newname = '你号啊 我是一个信纸'
console.log(obj)

console.log(Object.isFrozen(obj)) // 如果你设置了freeze 那么这里返回true说明你冻结了 否则返回false
```

### 13.fillter方法

```js
ages = [12,16,19,20]
function checknum(age){
    return age>=18
}
console.log(ages.fillter(checknum)) // [19,20]
// 如果有满足条件的返回数组 否则返回一个空数组
```

### 14 mouseenter & mouseleave

```js
// 鼠标穿过元素
$('#aph').mouseenter(function(){
    ...
})
// 鼠标离开元素
$('#aph').mouseleave(function(){
    ...
})
```

### 15 ${}

```js
// 以往的拼接字符串用 + 号
var aaa = '111'
'fcp${aaa}' // 这样就拼起来了
```

### 16 $t() 在vue中的作用

```js
// 在使用或者制作vue组件的时候我们需要将中文的数量降到最低 所以如果有中午需要出现我们可以抽离到一个文件中

// list.js
const list = {
	title:'你好啊'    
}

// 使用

{{$t(list.list.title)}}
```

### 17 Date

```js
  var d = new Date()
  console.log(d) // 打印当前时间

  var a = new Date(2012,1,11,1,1,1,1)
  console.log(a) // 打印你传入的具体时间 具体到毫秒

  var b = a.toString()
  console.log('toString'+b) // 就是打印时间

  var e = a.toUTCString()
  console.log(e) // 将时间转换未utc时间

  var f = a.toDateString()
  console.log(f) // 将时间转换未易读的方式

  // 日期格式化
  var s = new Date("2018/11/02")
  console.log(s)

  var k = s.getFullYear()
  console.log(k) // 返回年份 这里返回2018  getDate 月 分 秒 都是在get后面加上单词

  var o = s.setDate(11)
  console.log(o) // 这个是设置年份 你可以先获取一个年份然后设置其中的年月日等等 跟上面差不多
```

### 18 Math

```js
  // Math

  console.log(Math.PI) // 3.14......

  // 四舍五入
  console.log(Math.round(1.1)) // 打印 1
  console.log(Math.round(1.5)) // 打印 2

  // 次幂运算
  console.log(Math.pow(2,2)) // 打印4 2的2次幂

  // 开方
  console.log(Math.sqrt(9)) // 打印3 9开方

  //绝对值
  console.log(Math.abs(-11)) // 返回绝对值 这里打印11

  //上舍入 ceil
  console.log(Math.ceil(1.1))  // 打印2 向上摄入最近的整数

  // 下舍入 floor
  console.log(Math.floor(1.9)) // 打印1 向下舍入最近的整数

  // Math.min Math.max 获取一些数字中最大或者最小的数字 注意不是一个列表
  console.log(Math.min(1,2,3,4)) // 返回1
  console.log(Math.max(1,2,3,4)) // 返回4


  // 随机 random
  console.log(Math.random()) // 返回一个 0（包括）到 1（不包过）
  // 如果想返回一个0-多少的 就用下面这个方法
  console.log(Math.floor(Math.random() * 10)) // 返回一个0-9中随意一个整数
  // 如果返回1-多少的就用下面这个
  console.log(Math.floor(Math.random() * 10 )+1) // 返回一个1-10随意一个整数
  // 封装一个方法 用于返回一个 min 到max(不包括) 的一个数字
  function getRndInteger(min, max) {
    return Math.floor(Math.random() * (max - min) ) + min;
  }
```

### 19 正则

```js
  // 正则

  // 1. search()方法 返回你要匹配字符串的下标index
  var str = "Visit W3School!";
  var n = str.search("W3School");
  console.log(n) // 打印6

  // 在search中使用正则
  var str1 = "Visit W3School";
  var n1 = str.search(/w3school/i); // i的意思是不区分大小写

  // 2.replace()
  var str2 = "abc456"
  var n2 = str2.replace('abc','def') // replace也接受一个字符串来搜索 找到abc将它替换未def
  console.log(n2) // 打印def456

  // 在replace()中使用正则
  var str3 = "Visit Microsoft!";
  var res = str3.replace(/microsoft/i, "W3School");
  console.log(res) // 打印Visit W3School!

  // 正则表达式 修饰符
  // 1. i 就是不区分大小写
  // 2. g 就是全局搜索 举个例子
  var t1 = /is/g
  var tr1 = 'Is myis tois'
  var res1 = tr1.match(t1)
  console.log(res1) // 打印 (2)["is", "is"]
  // 3. m 多行匹配 举例
  var str4 = "\nIs th\nis it? \nis";
  var pat1 = /^is/m;
  var result = str4.match(pat1);
  console.log(result) // is 对每行的开始搜索is 如果有就返回is

  // 正则表达式模式
  // 1. [abc] 查找括号中的所有字符 举例
  var str5 = "Is this all there is?";
  var patt5 = /[t]/g;
  var result1 = str5.match(patt5);
  console.log(result1) // 打印 t,t t在str5中出现了两次 这是全局搜索 如果是i的话那么就返回一个t

  // 2. [0-9] 查找0-9中的数字
  var str6 = "123456789";
  var patt6 = /[1-4]/g;
  var result6 = str6.match(patt6);
  console.log(result6) // 打印1,2,3,4

  // 3.查找 字符串中有green或者有red
  var str7 = "re, green, red, green, gren, gr, blue, yellow";
  var patt7 = /(red|green)/g;
  var result7 = str7.match(patt7);
  console.log(result7) // 打印 green red green

  // 元字符
  // 1.\d 对字符串中的数字进行查找
  var str8 = "Give 100%!";
  var patt8 = /\d/g;
  var result8= str8.match(patt8);
  console.log(result8) // 打印1,0,0  如果改为 /d+ 则是100

  // 2.\s 对字符串中的空格进行查找
  var str9 = "Is this all there is?";
  var patt9 = /\s/g;
  var result9 = str9.match(patt9);
  console.log(result9) // , , ,  这说明匹配到了 里面有三个空格

  // 3.\b 单词的边缘匹配
  var str10 = "Visit W3Schools";
  var patt10 = /\bW3/g;
  var result10 = str.match(patt10);
  console.log(result10) // 对单词的开头或者结尾进行边缘搜索 这里打印W3

  // 定义量词 + * ?
  // 1.+
  var str11 = "Hellooo World! Hello W3School!";
  var patt11 = /o+/g;
  var result11 = str11.match(patt11); // 对字符串中出现的至少一个o进行全局查找 如果是i 那么就找第一次符合要求的 ooo 后面的不看了

  // 2.*
  var str12 = "Hellooo World! Hello W3School!";
  var patt12 = /lo*/g;
  var result12 = str12.match(patt12); // 全局搜索“l”，后跟零个或多个“o”字符
  console.log(result12) // 打印 l,looo,l,l,lo,l

  // 3.?
  var str13= "1, 100 or 1000?";
  var patt13 = /10?/g;
  var result13 = str13.match(patt13); // 全局搜索“1”，后跟零或一个“0”字符
  console.log(result13) // 打印1,10,10
```

### 20 RegExp(看视频补充)

```

```

### 21 异常

#### 21.1 简单使用 try catch

```html
<p id="demo"></p>
<script>
    try {
        adddlert("欢迎访问！");
    }
    catch(err) {
        document.getElementById("demo").innerHTML = err.message;
    }
    // 页面的p元素中会有 adddlert is not defined
</script>
```

#### 21.2 使用throw

```html
<html>
<body>
<p>请输入 5 - 10 之间的数字：</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">测试输入</button>
<p id="message"></p>
<script>
function myFunction() {
    var message, x;
    message = document.getElementById("message");
    message.innerHTML = "";
    x = document.getElementById("demo").value;
    try { 
        if(x == "") throw "空的";
         if(isNaN(x)) throw "不是数字";
         x = Number(x);
        if(x < 5) throw  "太小";
        if(x > 10) throw "太大";
    }
    catch(err) {
        message.innerHTML = "输入是 " + err;
    }
}
</script>
</body>
</html> 
```

#### 21.3 finally

```js
// finally 语句允许您在 try 和 catch 之后执行代码，无论结果
try {
     供测试的代码块
}
 catch(err) {
     处理错误的代码块
} 
finally {
     无论 try / catch 结果如何都执行的代码块
}
```

#### 21.4 error对象

1. 属性值
   1. error.name 设置或返回错误名
   2. error.message
2. 错误名

| 错误名         | 描述                          |
| -------------- | ----------------------------- |
| EvalError      | 已在 eval() 函数中发生的错误  |
| RangeError     | 已发生超出数字范围的错误      |
| ReferenceError | 已发生非法引用                |
| SyntaxError    | 已发生语法错误                |
| TypeError      | 已发生类型错误                |
| URIError       | 在 encodeURI() 中已发生的错误 |

### 22 严格模式

```
"use strict" 指令
"use strict" 是 JavaScript 1.8.5 中的新指令（ECMAScript version 5）。

它不算一条语句，而是一段文字表达式，更早版本的 JavaScript 会忽略它。

"use strict"; 的作用是指示 JavaScript 代码应该以“严格模式”执行。

在严格模式中，您无法，例如，使用未声明的变量。
```

### 23 const

```js
// 您可以创建 const 对象：
const car = {type:"porsche", model:"911", color:"Black"};

// 您可以更改属性：
car.color = "White";

// 您可以添加属性：
car.owner = "Bill";


// 常量无法修改
```

### 24 JSON

```js
// JSON 数据是从web服务器获取的数据

// JSON.parse
"{"name":"dmy"}"
var obj = JSON.parse("{"name":"dmy"}") // 将字符串转换为javascript对象
console.log(obj.name) // dmy

// JSON.stringify
// 当你想将数据发送给服务端 需要使用这个方法
  var obj = {"name":"Bill", "age":62, "city":"Seatle"};
  var myJSON = JSON.stringify(obj);
  console.log(typeof myJSON) // string
```

### 25 Promise

```js
// Promise 中扔进去的都是网络请求或者一种异步的操作 但是真正处理的时候要放到then 当你异步操作中使用了resolve 就会去找then去执行后面的操作 然后如果有第二次那么就返回一个Promise
new Promise((resolve,reject)=>{
    // 第一网络请求
    setTimeout(()=>{
        resolve()
    },1000)
}).then(()=>{
    console.log('我是第一次网络请求的数据')
    return new Promise((resolve,reject)=>{
        // 第二次网络请求
        setTimeout(()=>{
            resolve()
        })
    })
}).then(()=>{
    console.log('我是第二次网络请求的数据')
    return new Promise((resolve,reject)=>{
        // 第三次网络请求
        setTimeout(()=>{
            resolve()
        })
    })
}).then(()=>{
    console.log('我是第三次网络请求的数据')
})


// 如果网络请求有参数 和失败信息的捕获
new Promise((resolve,reject)=>{
    // data是网路请求到的数据
    setTimeout((data,error)=>{
        resolve(data)
        reject(error)
    },1000)
}).then((data)=>{
    console.log(data)
// 当你请求发生错误 那么回调的时候会来找这个.catch中去执行
}).catch((error)=>{
    console.log(error)
})


// 三种状态
pending 进行
fulfilled 满足
Rejected 失败

// Promise的另一种写法
// 将成功与失败都放到then中 thne接收两个函数 一个成功一个失败
 new Promise((resolve,reject)=>{
     setTimeout(()=>{
         resolve('成功')
         reject('失败')
     })
 }).then(data=>{
     console.log(data)
 },err=>{
     console.log(err)
 })

// 简写
// 需求 在第一次放松网络请求之后的获取的数据 在处理的时候给数据加工然后给到第二次去处理

new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('aaa')
    })
}).then(res=>{
    console.log(res,'第一层处理')
    return res+'111' 
    // 这个就是简写实际上就是 return new Promise((resolve,reject)=>{resolve(res+'111')})
}).then(res=>{   // 这里的res 就是已经拼接好111的了
    console.log(res,'第二层处理')
    return res + '222' // 这里其实就是 aaa111222
}).then(res=>{
    console.log(res) // aaa111222
})



// all 方法
// 参数 是一个可迭代对象
// 需求 只有当两次网络请求全部完成之后才进行下面的操作
Promise.all([
    new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve('aaa')
        },2000)
    }),
    new Promise((resolve,reject)=>{
        setTimeout(()=>{
            resolve('bbb')
        },1000)
    }),
]).then(results=>{
    console.log(results) // ['aaa','bbb']
})
// Promise.all 例子
// 如果全都为成功
function fn(time) {
  return new Promise((resolve, reject) => {
    console.log(88)
    setTimeout(() => {
      resolve(`${time}毫秒后我成功啦！！！`)
    }, time)
  })
}

Promise.all([fn(2000), fn(3000), fn(1000)]).then(res => {
  // 3秒后输出 [ '2000毫秒后我成功啦！！！', '3000毫秒后我成功啦！！！', '1000毫秒后我成功啦！！！' ]
  console.log(res) 
}, err => {
  console.log(err)
})



// 如果有一个失败
function fn(time, isResolve) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      isResolve ? resolve(`${time}毫秒后我成功啦！！！`) : reject(`${time}毫秒后我失败啦！！！`)
    }, time)
  })
}

Promise.all([fn(2000, true), fn(3000), fn(1000, true)]).then(res => {
  console.log(res)
}, err => {
  console.log(err) // 3秒后输出 '3000毫秒后我失败啦！！！'
})


// race
function fn(time, isResolve) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      isResolve ? resolve(`${time}毫秒后我成功啦！！！`) : reject(`${time}毫秒后我失败啦！！！`)
    }, time)
  })
}

Promise.race([fn(2000, true), fn(3000), fn(1000)]).then(res => {
  console.log(res)
}, err => {
  console.log(err) // 1秒后输出
})





// 红绿黄灯 题目
function red(){
    console.log('red');
}
function green(){
    console.log('green');
}
function yellow(){
    console.log('yellow');
}

var light = function(timmer, cb){
    return new Promise(function(resolve, reject) {
        setTimeout(function() {
            cb();
            resolve();
        }, timmer);
    });
};

var step = function() {
    Promise.resolve().then(function(){
        return light(3000, red);
    }).then(function(){
        return light(2000, green);
    }).then(function(){
        return light(1000, yellow);
    }).then(function(){
        step();
    });
}

step();

// Promise.finally()
function abc(time=1000){
    return new Promise((resolve,reject)=>{
        setTimeout(function(){
            resolve(time)
        },time)
    })
}

abc()
.then(res=>{console.log(res)})
.catch(err=>{console.log(err)})
.finally(()=>{console.log('我是finally')})
// 不管 Promise 是否成功 都会执行finally
```

### 26 强转

```js
// toString 只适用于 布尔 数值 字符串
// 该方法不会直接影响原值而是返回一个值
var a = 123
var b = a.toString(); // b是string
a = a.toString()

// 对于布尔值来说
var a = true
a = a.toString() // a-> "true" 可以转过来

// 如何转 null 还是 undefined呢？ String() 这个方法也是返回一个值
var a = null
a = String(a) // a -> "null" string类型 undefined和他一样

// Number()
// true 转number是1 false为0
// null 转为0
// undefined 转为 NaN 就是转不了
// 'foo' 这种 会直接转换为NaN


// parseInt() 可以将一个字符串中有效的整数内容取出来转换为number 从这个字符串左边往右边解析
var a =123a567
parseInt(a) // 123

var a = b123567
parseInt(a) // NaN

var a = 123.456
parseInt(a)  // 123


// parseFloat()
var a = 123.456a
parseFloat(a) // 123.456


// 注意 如果是布尔类型这种 会先转为字符串然后再进行操作
var a = true
parseInt(a) // 先为 "a" 然后转  NaN


// 任何值 和 NaN 做运算都是 NaN
```

### 27 布尔值

```js
var b = 10
!b // false
!!b // true
// 可以对一个非布尔值 转换为一个布尔值


// && ||  &&比|| 优先级高
// 1 && 2  运算的时候会转换为布尔值进行计算 如果两边的为true的话会返回后面的那个
// 0 && 2  运算的时候会直接返回0  2 && 0 会返回0

// 1 || 2  如果第一个值是true 则直接返回第一个值
// 0 || 2  如果第一个值是false 则返回第二个值
// 0 || 0  如果都是false 返回第二个值

console.log(Boolean(new Boolean(false))) // true
```

### 28 比较

```js
// 如果比较运算符两侧都是字符串 会比较两个字符串的Unicode 编码 它会一位一位的进行比较
'bbc' < 'b' // 先 b 和b 然后 b和右边的第二个进行比较 第二个是没有的 所有左边大


// 当使用 == 来进行比较时 如果两个类型不一样 则会转换为相同的类型进行比较
console.log('1' == 1) // '1' 转换为数字 !=也会进行类型转换

// NaN 不和任何值相等 包括它本身 如果我们想判断一个值是否为NaN呢？ isNaN()
var n = NaN
isNaN(n) // true
```

### 29.对象

```js
var obj = new Object()
// 使用new关键字调用的函数 是构造函数constructor

// 删除对象的属性
delete obj.name // 删除obj的name属性

// 如果想用123 当属性名不能用.的方式
obj["123"] = 789
console.log(obj["123"]); // 取得时候也必须用这种[]方式

// js属性值可以是任意得数据类型

// in 得使用 检查对象中是否有这个属性
console.log('name' in obj1) // 属性名必须是字符串类型


// 引用数据类型 -》 对象 
var obj = new Object()
var obj2 = obj
// 因为在栈存储得时候 如果是对象则存得是内存地址 所以这俩是一个内存地址 修改得时候会相互影响
var obj2 = null // obj2 不指向这个内存地址了 obj不会受到影响

// 基本数据类型
var a = 1
var a1 = a
// 这种基本数据类型不会相互影响

// 对象字面量
var obj = {} // {}为一个对象字面量 使用对象字面量可以直接在字面量中定义属性
```

### 30.函数

```js
// 自执行函数
(function (){
    console.log('立即执行')
})();
// 给function 套一个() 是为了让编译器知道这是一个函数 不加得话 它不认识

// 函数return 如果不给值 或者没有写return 那么就是undefined
```

### 31 全局作用域

```js
// 全局作用域是写在script标签中的js代码 
// 页面打开得时候创建 页面关闭时被销毁
// 创建得标量作为window对象得属性值被保存
// 创建得函数作为window对象得方法被保存

1.变量得声明提前
// 所有得var 定义变量时 都会提前声明但是不会赋值 只有到赋值得那一行才会执行赋值操作 var操作都会在最前面被执行

2.函数得声明提前
fun1() // 不会被执行 因为var会在最开始声明 但是函数没有定义出来 只有到那一行就是12行被定义函数
fun2() // 函数声明得形式声明函数 会在最开始就声明出来整个函数 所以是可以调用得
var fun1 = function(){
    console.log('我时fun1')
}

fun2(){
    console.log('我是fun2')
}
```

### 32 函数作用域

```js
// 函数的提前声明
function fun1(){
    fun2() // alert('hello') fun2()会在函数作用域的所有代码之前被执行所以是可以进行调用执行
    function fun2(){
        alert('hello')
    }
}

function fun1(){
    console.log(a) // undefined 因为var操作会在函数作用域最开始执行 然后定义是在第10行定义
	var a = 1
}

// 因为JS采用的是静态作用域 看这个例子
var value = 1;

function foo() {
    console.log(value);
}

function bar() {
    var value = 2;
    foo();
}

bar(); // 1
// 操作顺序 执行bar()函数 然后执行里面的foo()函数 foo函数中要打印value 因为是静态作用域 就根据其书写的位置找到上一层 是window 并且找到了value值 所以打印1

// 再看一个例子
var scope = "global scope";
function checkscope(){
    var scope = "local scope";
    function f(){
        return scope;
    }
    return f;
}
checkscope()(); // 打印 local scope 这也印证了 作用域是在函数定义的位置 此时f函数定义在checkscope的里面 执行的时候首先找自己 自己是没有的 所以找到上面一层也就是checkscope作用域 所以打印local scope
```

### 33 工厂方法

```js
function createPerson(name,gender){
    var obj = new Objcet()
    obj.name = name
    obj.gender = gender
    
    return obj
}

var obj1 = createPerson('杜梦越','男')
var obj2 = cratePerson('dmc','男')
```

### 34 构造函数

```js
// 构造函数首字母大写不是硬性要求 但是这是规范
// 构造函数执行过程
    1.立即创建一个新对象
    2.将新对象设置为函数中的this,在构造函数中可以用this来引用新建的对象
    3.逐行执行函数中的代码
    4.将新建的对象作为返回值返回

    
// 举例
function Person(name,age){
    this.name = name
    this.age = age
}    
var person1 = new Person('dmy','11')


function Dog(name,age){
    this.name = name
    this.age = age
}
var dog1 = new Dog('dmy','11')

console.log(person1) // Person { name:'dog' , age:'11' }
console.log(dog1)    // Dog { name:'dog' , age:'11' }

console.log(person1 instanceof Person) // true
console.log(dog instanceof Person) // false
console.log(person1 instanceof Object) // true
```

### 35 原型

```js
// 简单使用
    function Person(name,age){
        this.name = name
        this.age = age
    }

    // 如果需要实例化很多次这个Person创建实例对象 那么对象中的有些方法是共用的 那么你每实例化一次就会多一个 很占内存 所以这里引出原型
    Person.prototype.sayHello = function(){
        console.log('大家好我是一个人哦'+this.name)
    }
    
    var person1 = new Person('dmy',11)
    person1.sayHello() // 打印大家好我是一个人哦dmy

    var person2 = new Person('dmc',12)
    person2.sayHello() // 打印大家好我是一个人哦dmc

    console.log(person1.__proto__.sayHello == Person.prototype.sayHello) // true
    /*
        由上可知，如果你在构造函数的原型上定义一个sayHello 那么这就是个公用的方法 所有实例化的对象是可以访问到的
        以后如果有很多公用的方法或者属性可以定义在这个原型上面
        补充：像hasOwnProperty 这种是原型的原型中的一个方法 那么什么时候到头呢就是Object对象就是祖先
        实例与原型的关系
        	当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。
    */


// 补充
  function Person(name){
    this.name = name
  }
  var person1 = new Person()
  console.log(person1.__proto__ == Person.prototype) // true
  Person.prototype = {
    msg: '新的原型'
  }
  console.log(person1.__proto__ == Person.prototype) // false

/*
	我们知道 构造函数的原型 是和 实例对象的原型是一样的 但是如果你以字面量的形式更改了构造函数的原型 这时候实例对象的原型并没有随之改变 还是指着原来的原型
*/
```

<img src="C:\Users\myduh\Desktop\原型.png" alt="原型"  />



### 36 数组

```js
var arr1 = new Array(10) // 创建一个长度为10的数组

// 字面量形式创建数组
var arr1 = []

// push
result = arr1.push('1','2')
console.log(result) // 2 返回push后的长度

// pop
var result = arr2.pop()
console.log(result) // pop 会返回以删除的那个值

// forEach
/*
 forEach方法 此方法需要我们传入一个回调函数它会自动执行 并且我们可以用三个形参去接收参数
     第一个参数为值 也就是每一次遍历数组的那个值
     第二个参数为索引 对应的就是那个值的索引
     第三个值是原数组
*/
var arr = [1,2,3,4,5]
arr.forEach((value,index,array)=>{
    console.log('值为'+value)
    console.log('索引为'+index)
    console.log('arrar为'+array)
})

// slice
    var arr = [1,2,3,4]
    // slice 取数组中的一些值
    //      - 第一个参数 从哪开始 包含这个值
    //      - 第二个参数 从哪结束 不包含这个值  比如 arr.slice(1,3) 取出1到2 3不包括
    var res = arr.slice(1,2)
    console.log(res)

    // 可以是负值 -1就是数组的倒数第一个 -2 就是倒数第二个
    arr.slice(1,-1)
	
	// 补充 将一个对象转换为一个数组
	  var a = {
        0:'name',
        1:'age',
        length: 2  // 必须有这个属性
      }
      var b = Array.prototype.slice.call(a)
      console.log(b) // ['name','age']


// concat

    var arr = [1,2,3,4]
    var arr1 = [5,6,7]

    // concat 不会对原数组造成影响 而是返回一个新的数组
    var res = arr.concat(arr1,'dmy','dmc')
    console.log(res) // [1, 2, 3, 4, 5, 6, 7, "dmy", "dmc"]

// join
    // join 将数组中的元素连起来 该方法也不会对原数组造成影响
    // 如果你什么都不传 则默认用逗号 注意 你传一个空字符串也是传了 我说的是里面什么都没有的情况
    var res1 = arr1.join()
    console.log(res1) // 5,6,7
    var res2 = arr1.join('') 
    console.log(res2) // 567

// sort
/*
	该方法不要直接使用对数组中全是数字的数组进行排序因为它会根据Unicode编码进行排序
	
	规则：sort()里面写一个回调函数 两个值
		 返回1就是交换位置
		 返回0就是两个值相等不进行操作
		 返回-1就是不交换位置
*/
    var arr3 = [3,7,1,5,2,9,0]
    arr3.sort((a,b)=>{
        // 如果你希望是升序
        return a-b // 如果a小于b 那么值为负的,不进行操作;如果大于0那么就要交换,小的交换到前面
        // 如果你希望是降序
        return b-a // 如果后面的值大于前面的值则大的值交换到前面
    })

// shift 弹出数组中第一个 会改变数组 返回值就是这个被弹出的

var a = [1,2,3]
var b = a.shift()
console.log(b) // 打印1
console.log(a) // 打印 [2,3]

// Array.from 可以将一个类数组或者一个对象转换为一个数组
// 它的第二个参数是一个回调函数 每次循环一个元素会将元素作为参数传入这个回调函数中 然后返回一个值
console.log(Array.from('foo'));
// expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], x => x + x));
// expected output: Array [2, 4, 6]
```

### 37.apply 与 call

```js
    function a(){
        console.log(this)
    }
    var obj = {name:'dmy',age:'11'}
    a.apply(obj) // 将a这个函数的this更改为obj的this 打印{name: "dmy", age: "11"}
    a.call(obj)  // 这里call 和 apply效果是一样的

    var obj2 = {
        sayName:function(){
            console.log(this)
        }
    }
    obj2.sayName.apply(obj) // 打印 {name: "dmy", age: "11"} 将this改为了obj的this

    // call
    function b(a,b){
        console.log('a' + a)
        console.log('b' + b)
    }
    b.call(obj,1,2) // 将b的this 变为obj的this 并且如果b这个函数需要传入参数可以在后面将参数带上

    // apply

    b.apply(obj,[1,2]) // apply 如果也想传参需要将传入的参数封装到一个数组中


// apply 补充
  function Otaku (name, age) {
    this.name = name;
    this.age = age;
    this.habit = 'Games';
  }
  var obj = new Object()
  Otaku.call(obj) 
  console.log(obj) // 打印 {name:"undefined",age:"undefined",habit:"Games"}

// apply 补充2
function cat(){
    
}
cat.prototype={
    food:"fish",   
    say: function(){      
         alert("I love "+this.food);
    }
}
var blackCat = new cat;
blackCat.say(); // 此时我们可以通过实例对象blackCat 来调用say方法
// 但是 当有一个 狗对象
WhiteDog = {
    food: 'cheas'
}
// 我们不想写一个say方法 我们就想要cat的 咋办呢？
blackCat.say.apply(WhiteDog)

// 对于一个类数组也一样 类数组是无法直接调用 push 或者 slice这种的 如果我们就是想用呢？
Array.prototype.slice.call(类数组)
```

### 38 arguments

```js
// 这个参数是一个函数中隐性的 它可以得到你传入函数的参数 还有它是一个伪数组可以得到长度

function a(){
    console.log(arguments.length)
}
a('11','22') // 打印2 因为你传入了两个参数

function b(){
    console.log(arguments[0])
}
b('11') // 打印11 arguments[0] 可以取到你传入参数的第一个参数
```

### 39 寻找值与索引的方法 ES6新增

```js
  let arr = [1,2,3,4,5]
  const ida = arr.find(item=>item===4) // 返回找到的值
  const id = arr.findIndex(item=>item===4) // 返回找到的值对应的索引
  console.log(id,ida) // 3,4

  let arr1 = [
    {name:'杜梦越',age:11},
    {name:'杜梦超',age:12}
  ]
  const bta = arr1.find(({name})=>name=='杜梦越') // 利用解构 因为回调中参数就是每个元素 从元素抽取name
  const btb = arr1.findIndex(({name})=>name==='杜梦越') // 返回对应的索引
  console.log(bta,btb) // {name:'杜梦越',age:11},0
```

### 40 关于数值 ES6新增

```js
// isInteger()
Number.isInteger(10);        // 返回 true
Number.isInteger(10.5);      // 返回 false

// isNaN() 如果是数值返回false 如果是非数值返回true
```

### 41 对象中的 setter 和getter

```js
// getter
var person = {
  firstName: "Bill",
  lastName : "Gates",
  get fullName() { // 注意这压力
    return this.firstName + " " + this.lastName;
  }
};

// 使用 getter 来显示来自对象的数据：
document.getElementById("demo").innerHTML = person.fullName;


// setter
var person = {
  firstName: "Bill",
  lastName : "Gates",
  language : "",
  set lang(lang) {
    this.language = lang.toUpperCase();
  }
};

// 使用 setter 来设置对象属性：
person.lang = "en";

// 显示来自对象的数据：
document.getElementById("demo").innerHTML = person.language;
```

### 42 ...的使用（未完成）

```js
// 简单使用
// 相当于apply方法 先举一个apply的例子
function fun1(a,b){
    return a + b
}
fun1.apply(null,[1,2]) // this不更改只想 给fun1传入数组作为a,b的参数

// 使用...
var args = [1,2]
fun1(...args) // ...后面跟一个可迭代对象 ...[1,2,3,4,5] 这样也可以 不用非得声明一个变量

// 构造字面量数组时
var parts = ['shoulders', 'knees']; 
var lyrics = ['head', ...parts, 'and', 'toes']; 
// ["head", "shoulders", "knees", "and", "toes"]

// 构造字面量对象时使用
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };
var clonedObj = { ...obj1 };
// 克隆后的对象: { foo: "bar", x: 42 }
var mergedObj = { ...obj1, ...obj2 };
// 合并后的对象: { foo: "baz", x: 42, y: 13 }
```

### 43 Timing事件

```js
// 1.setTimeout
// 单击按钮。等待 3 秒，然后页面会提示 "Hello"：
function myFunction() {
    alert('Hello');
}
var time1 = setTimeout(myFunction,3000) // 三秒后执行该代码


// 如何取消这个定时呢
clearTimeout(time1) // 取消这个定时

// 2.setInterval
window.setInterval(function, milliseconds);
// 第一个参数 是要执行的函数
// 第二个参数 是多少秒之后执行一次这个函数(重复)
var myVar = setInterval(myTimer, 1000);
function myTimer() {
    var d = new Date();
    document.getElementById("demo").innerHTML = d.toLocaleTimeString();
}

// 如何停止呢？
clearInterval(myVar);
```

### 44 变量对象

```js
/*
进入执行上下文
1.
当进入执行上下文时，这时候还没有执行代码
变量对象会包括：
函数的所有形参 (如果是函数上下文)
由名称和对应值组成的一个变量对象的属性被创建
没有实参，属性值设为 undefined
2.
函数声明
由名称和对应值（函数对象(function-object)）组成一个变量对象的属性被创建
如果变量对象已经存在相同名称的属性，则完全替换这个属性
3.
变量声明
由名称和对应值（undefined）组成一个变量对象的属性被创建；
如果变量名称跟已经声明的形式参数或函数相同，则变量声明不会干扰已经存在的这类属性
*/

// 举例
function foo(a) {
  var b = 2;
  function c() {}
  var d = function() {};
  b = 3;
}
foo(1);

// 1.进入上下文的阶段
AO = {
    arguments: {
        0: 1,
        length: 1
    },
    a: 1, // 因为实参a是有传递参数的 所以这里是1
    b: undefined,
    c: reference to function c(){},
    d: undefined
}
// 2.代码执行
// 顺序执行 修改变量对象的值
AO = {
    arguments: {
        0: 1,
        length: 1
    },
    a: 1,
    b: 3,
    c: reference to function c(){},
    d: reference to FunctionExpression "d"
}

// 第一题
function foo() {
    console.log(a);
    a = 1;
}

foo(); // 报错 a并没有存放在AO中 所以没有a然后去全局找也没有 所以就报错了

function bar() {
    a = 1;
    console.log(a);
}
bar(); // 1 a被定义在了全局中 所以可以找到它

// 第二题
console.log(foo); // 打印函数foo的信息 这是因为在执行上下文时首先会处理函数的声明其次才是变量的 又因为如果出现变量和函数名称相同的 那么变量的名称是不会改变函数的

function foo(){
    console.log("foo");
}

var foo = 1;
```

### 45 闭包

```js
// 先看一个经典的题目
var data = [];

for (var i = 0; i < 3; i++) {
  data[i] = function () {
    console.log(i);
  };
}

data[0]();
data[1]();
data[2]();
// 这里都会打印多少呢？ 并不是012 而是2 都是2

// 利用闭包
var data = [];

for (var i = 0; i < 3; i++) {
  data[i] = (function (i) {
        return function(){
            console.log(i);
        }
  })(i);
}
// 当循环执行的时候 首先匿名函数有一个形参i 这里是自执行 第一次循环的时候 将0作为参数传入匿名函数 也就相当于有了一个实参 var i = 0 然后返回一个函数 这个函数打印i首先它是没有i的 但是这个函数定义的时候 它有了上层匿名函数的AO 这里是有i 又因为我们之前已经定义好了 实参i=0 所以这里打印0 那么之后的 1 2 都是这个原理

data[0]();
data[1]();
data[2]();
```

### 46 按值传递

```js
// 例子1
var value = 1;
function foo(v) {
    v = 2;
    console.log(v); //2
}
foo(value);
console.log(value) // 1

// value 指向常量区中的 1
// v = value 那么 v也指向常量区中的1
// v=2 这时候改变 v的指向 指向2 所以打印v的时候是2
// value 指向一直没变 还是1

// 例子2
var obj = {
value: 1
};
function foo(o) {
    o.value = 2;
    console.log(o.value); //2
}
foo(obj);
console.log(obj.value) // 2

// obj 指向一个 Object对象 而o也指向这个Object对象 所以当修改 o.value 那么堆内存的这个Object的属性value就会改变 o.value的值发生了指向的改变 从指着1到2 而o并没有

// 例子3
var obj = {
value: 1
};
function foo(o) {
    o = 2;
    console.log(o); //2
}
foo(obj);
console.log(obj.value) // 1

// obj 指向堆内存中的Object {value:1} 而给形参o传递了实参obj o = obj 那么俩人现在是都指着Object的 但是函数中改变了o的指向 将指向改为了常量区中的2 但是object并没有改变 所以 obj没有变
```

### 47 bind的使用

```js
/*
bind() 方法会创建一个新函数。当这个新函数被调用时，bind() 的第一个参数将作为它运行时的 this，之后的一序列参数将会在传递的实参前传入作为它的参数。(来自于 MDN )
*/
// 1.第一个例子
var foo = {
    value: 1
};
function bar() {
    console.log(this.value);
}
// 返回了一个函数
var bindFoo = bar.bind(foo);  // 改变了bar的this指向 并且返回了一个新的函数 而不是像apply和call直接执行

bindFoo(); // 1
```

### 48 类数组

```js
/*
 类数组是无法使用数组的方法的 其他的像遍历 通过[]取值 是一样的
*/

var arrayLike = {0:'name',1:'age'}
// [] 获取值
arrayLike[0] => name
arrayLike[1] => age

// 遍历
for(var i=0,len=arrayLike.length;i<len;i++){
    ....
}

// 方法 
arrayLike.push('4'); // 直接报错 arrayLike.push is not a function


// 解释类数组
function a(b,c,d){
    console.log(arguments)
}
a(1,2,3)
/*
打印
	0: 1
    1: 2
    2: 3
    callee: ƒ a(b,c,d)
    length: 3
    Symbol(Symbol.iterator): ƒ values()
    [[Prototype]]: Object
    
    
    1. length 指的是实参的长度 这里有三个形参并且传递了三个实参所以长度为3 如果只传了1个那么打印1
    2. a.length 是a的形参的长度为3
    3. callee => Arguments 对象的 callee 属性，通过它可以调用函数自身。
    	利用经典闭包
    	var data = [];
        for (var i = 0; i < 3; i++) {
            (data[i] = function () {
               console.log(arguments.callee.i) 
            }).i = i;
        }
        data[0]();
        data[1]();
        data[2]();
*/

// 补充几个类数组转为数组的方法
var arrayLike = {0: 'name', 1: 'age', 2: 'sex', length: 3 }
// 1. slice
Array.prototype.slice.call(arrayLike); // ["name", "age", "sex"] 
// 2. splice
Array.prototype.splice.call(arrayLike, 0); // ["name", "age", "sex"] 
// 3. ES6 Array.from
Array.from(arrayLike); // ["name", "age", "sex"] 
// 4. apply
Array.prototype.concat.apply([], arrayLike)
// 5. ES6转换
function a(...arguments){
    console.log(arguments) // [1,2,3]
}
a(1,2,3) 
```

### 49 继承

```js
// 最常用的继承方式
function Parent (name) {
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}
Parent.prototype.getName = function () {
    console.log(this.name)
}
function Child (name, age) {
    Parent.call(this, name);
    this.age = age;
}
Child.prototype = new Parent();
Child.prototype.constructor = Child;

var child1 = new Child('kevin', '18');

child1.colors.push('black');

console.log(child1.name); // kevin
console.log(child1.age); // 18
console.log(child1.colors); // ["red", "blue", "green", "black"]

var child2 = new Child('daisy', '20');

console.log(child2.name); // daisy
console.log(child2.age); // 20
console.log(child2.colors); // ["red", "blue", "green"]
```

### 50 防抖与节流

```js
// 防抖
/*
	防抖的原理就是：你尽管触发事件，但是我一定在事件触发 n 秒后才执行，如果你在一个事件触发的 n 秒内又触发了这个事件，那我就以新的事件的时间为准，n 秒后才执行，总之，就是要等你触发完事件 n 秒内不再触发事件，我才执行，真是任性呐!
*/

// 第一版
function debounce(func, wait) {
    var timeout; // 这里利用闭包 初始化了一个timeout 把它存在内存中
    return function () {
        clearTimeout(timeout)
        timeout = setTimeout(func, wait);
    }
}
container.onmousemove = debounce(getUserAction, 1000);
// 鼠标经过事件 当鼠标经过时 触发防抖返回的那个函数 先清除定时器 然后设置一个定时器多少秒之后触发你传入的函数 如果你又触发了鼠标经过事件 就会先清楚定时器 然后又设置一个新的

// 第二版 this问题
function debounce(func, wait) {
    var timeout;
    return function () {
        var context = this;
        clearTimeout(timeout)
        timeout = setTimeout(function(){
            func.apply(context)
        }, wait);
    }
}
// 注意这里的例子时基于 一个div 然后获取这个div 给这个div一个鼠标滑过事件 那么当你给这个div绑定的时候 不适用防抖 那么你在事件里面打印this 会打印 div那个元素 但是如果你用了防抖第一版的时候 this就为window了 所以需要修改一下指向  返回函数的时候 先获取一个this 这个this就是 那个元素的this 然后执行的事件 将this指向元素的this

// 第三版 关于事件event
function debounce(func, wait) {
    var timeout;

    return function () {
        var context = this;
        var args = arguments; // 这里 默认会将鼠标滑过事件event传入的
        clearTimeout(timeout)
        timeout = setTimeout(function(){
            func.apply(context, args) // 将事件传入func
        }, wait);
    }
}

// 第四版 
// 需求：我希望立即执行 而不是执行一次要等多少秒 比如第一次滑过执行 然后等一会之后再滑过又立即执行
function debounce(func, wait, immediate) {
    var timeout;
    return function () {
        var context = this;
        var args = arguments;
        if (timeout) clearTimeout(timeout); 
        if (immediate) { 
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            }, wait)
            if (callNow) func.apply(context, args)
        }
        else {
            timeout = setTimeout(function(){
                func.apply(context, args)
            }, wait);
        }
    }
}
/*
过程: 
	第一次执行timeout是false所以不走清除定时器，判断immediate是否为true这里假设是true，那么callNow为true，设置一个定时器将timeout清空 此时callNow为true 第一次直接执行了
	第二次 当你还没有等到定时器执行的时候你马上执行了第二次 这时候你的timeout是true 将它清空并且进入if语句 此时的callNow为false 因为你是有timeout的这时候 并且重新设置一个定时器timeout 里面将timeout设置为null 那么这时候你也不会执行函数 因为callNow是false
	第三次 如果你等待了这个定时器清空了 那么此时你的timeout就为 null了 你不会进行清楚这一步 然后进入if语句 callNow为true 然后设置一个定时器 然后立刻执行代码
*/ 



// 节流
/*
	什么是节流？当你持续触发一个事件的时候会设置一个周期 比如刚开始是0 你设置了5秒，那么你在这五秒之内一直触发是不会一直执行的 只有到了五秒才触发 然后将时间设置为这个五秒 然后在往后推到10秒 如果你还想执行 在5-10秒之间一直执行时没用的 要等到十秒的时候
	
	以上是我的说法 看下github上的
	节流的原理很简单：
        如果你持续触发事件，每隔一段时间，只执行一次事件。
        根据首次是否执行以及结束后是否执行，效果有所不同，实现的方式也有所不同。
        我们用 leading 代表首次是否执行，trailing 代表结束后是否再执行一次。
        关于节流的实现，有两种主流的实现方式，一种是使用时间戳，一种是设置定时器。
*/
// 第一版 时间戳的方式
function throttle(func, wait) {
    var context, args;
    var previous = 0;

    return function() {
        var now = +new Date(); // 记录一下当前的时间
        context = this;
        args = arguments;
        if (now - previous > wait) { // 如果当前的时间减去之前的时间(刚开始是0) 大于你设置的节流周期时间
            func.apply(context, args); // 执行
            previous = now; // 更新之前的时间 为当前的时间
        }
    }
}

// 第二版 定时器的方式
function throttle(func, wait) {
    var timeout;
    var previous = 0;

    return function() {
        context = this;
        args = arguments;
        if (!timeout) { // 第一次触发 timeout为false
            timeout = setTimeout(function(){  // 设置一个定时器
                timeout = null; // 设置为null
                func.apply(context, args) // 触发事件
            }, wait)
        }
    }
}
// 当你还没到定时器的时间呢你又区触发了 那么这个时候不会有任何操作 因为timeout有值
// 当你等待这个timeout执行了 那么这个时候timeout就为null了 然后你再去触发事件 这个时候会重新设置一个定时器


// 结合版本
function throttle(func, wait) {
    var timeout, context, args, result;
    var previous = 0;
    
    var later = function() { // 此函数为最后一次执行时触发的函数
        previous = +new Date();
        timeout = null;
        func.apply(context, args)
    };

    var throttled = function() {
        var now = +new Date();
        //下次触发 func 剩余的时间
        var remaining = wait - (now - previous);
        context = this;
        args = arguments;
         // 如果没有剩余的时间了或者你改了系统时间
        if (remaining <= 0 || remaining > wait) {
            if (timeout) {
                clearTimeout(timeout);
                timeout = null;
            }
            previous = now;
            func.apply(context, args);
        } else if (!timeout) {
            timeout = setTimeout(later, remaining);
        }
    };
    return throttled;
}
/*
	补充：为什么要用闭包呢？
	1、对于一个页面上需要多个防抖函数的时候，需要写很多重复代码。
	2、全局变量污染作用域
	这时候闭包的优势就体现出来了，保护全局作用域不被污染,又能做到函数复用，我们只需要封装这么一个debounce函数就可以了
*/
```

### 51 数组去重

```js
function unique(array, isSorted, iteratee) {
    var res = [];
    var seen = [];

    for (var i = 0, len = array.length; i < len; i++) {
        var value = array[i];
        var computed = iteratee ? iteratee(value, i, array) : value;
        if (isSorted) {
            if (!i || seen !== computed) {
                res.push(value)
            }
            seen = computed;
        }
        else if (iteratee) {
            if (seen.indexOf(computed) === -1) {
                seen.push(computed);
                res.push(value);
            }
        }
        else if (res.indexOf(value) === -1) {
            res.push(value);
        }        
    }
    return res;
}

console.log(unique(array3, false, function(item){
    return typeof item == 'string' ? item.toLowerCase() : item
})); // [1, "a", 2]
/*
	array：表示要去重的数组，必填
    isSorted：表示函数传入的数组是否已排过序，如果为 true，将会采用更快的方法进行去重
    iteratee：传入一个函数，可以对每个元素进行重新的计算，然后根据处理的结果进行去重	
*/
```

### 52 Jquery中 extend的使用

```js
// 简单使用 合并两个或者更多的对象的内容到第一个对象中。
var a = {
    b:1,
    c:[1,2]
}
var b = {
    d:4,
    c:[2,3]
}
console.log($.extend(a,b)) // {b:1,c:[2,3],d:4}

// 如何更深层的拷贝的？ extend()的第一个
var obj1 = {
    a: 1,
    b: { b1: 1, b2: 2 }
};

var obj2 = {
    b: { b1: 3, b3: 4 },
    c: 3
};

var obj3 = {
    d: 4
}

console.log($.extend(true, obj1, obj2, obj3));

// {
//    a: 1,
//    b: { b1: 3, b2: 2, b3: 4 },
//    c: 3,
//    d: 4
// }
```

### 53 惰性函数

```js
/*
	需求：每次调用foo()的时候 只有第一次会生成一个Date对象
*/

function foo(){
    var t = new Date()
    foo = function(){
        return t
    }
    foo()
}
// 第一次执行的时候 将t变成一个Date对象 然后重写了foo()函数 最后执行这个foo函数 返回一个t
// 第二次执行 这时候 foo函数已经被我们重写了 所以你再执行 它只会返回t
```

### 54 ES6

#### 54.1 let 与 const

```js
// 1. let 和 const 是不绑定全局作用域的
var a = 1
console.log(window.a) // 1

let a = 1
console.log(window.a) // undefined const一样

// let 和 const 的临时死区
/*
	 JavaScript 引擎在扫描代码发现变量声明时，要么将它们提升到作用域顶部(遇到 var 声明)，要么将声明放在 TDZ 中(遇到 let 和 const 声明)。访问 TDZ 中的变量会触发运行时错误。只有执行过变量声明语句后，变量才会从 TDZ 中移出，然后方可访问。
*/
var value = "global";

// 例子1
(function() {
    console.log(value);
    let value = 'local';
}());
// 例子2
{
    console.log(value);
    const value = 'local';
};
// 两个例子都会报错Uncaught ReferenceError: value is not defined
```

#### 54.2 模板字符串

```js
/*
	模板字符串支持嵌入变量，只需要将变量名写在 ${} 之中，其实不止变量，任意的 JavaScript 表达式都是可以的：
*/

  // 将变量嵌套进去
  let a = '123'
  let msg = `<a>${a}</a>` // 注意 一定要用 `` 括起来
  console.log(msg)

  // JS 语句
  var arr = [{value:1},{value:2}]
  var msg = `
    <ul>
      ${arr.map((item)=>{
        return `<li>${item.value}</li>`
      })}
    </ul>
      `
  console.log(msg)
  // 函数
  	let x = 'Hi', y = 'Kevin';
    var res = message`${x}, I am ${y}`;
    console.log(res);
	// literals 文字
    // 注意在这个例子中 literals 的第一个元素和最后一个元素都是空字符串
    function message(literals, value1, value2) {
        console.log(literals); // [ "", ", I am ", "" ] 这里就是三个元素 头和尾都是一个空字符串 中间是内容
        console.log(value1); // Hi
        console.log(value2); // Kevin
    }
// 使用
    function message(literals, ...values) {
        let result = '';
        for (let i = 0; i < values.length; i++) {
            result += literals[i];
            result += values[i];
        }
        result += literals[literals.length - 1];
        return result;
    }
  	let x = 'Hi', y = 'Kevin';
    var res = message`${x}, I am ${y}`;
    console.log(res); // Hi, I am Kevin
```

#### 54.3 解构

```js
// 数组解构
let [a,b,c] = [1,2,3]
console.log(b) // 2

let [a,[b,c],d] = [1,[2,3],4]
console.log(c) // 3

let [x, y] = ['a'];
console.log(y) //undefined

let [x,y=1] = [2]
console.log(y) // 1 如果有默认值 没有解构给值就打印默认值

// 对象解构
/*
	对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
*/
let person = {name:'ddd',age:11}
const {name:name,age:age} = person // 属性与值必须相对应
console.log(name,age) // ddd 11
const obj = {
  name: '林三心',
  age: 22,
  gender: '男',
  doing: {
    morning: '摸鱼',
    afternoon: '摸鱼',
    evening: 'sleep'
  }
}

const { name, age, gender } = obj
console.log(name, age, gender) // 林三心 22 男

// 解构重名
const { name: myname } = obj
console.log(myname) // 林三心

// 嵌套解构
const { doing: { evening } } = obj
console.log(evening) // sleep
// 对象解构end

// 字符串解构
let str1 = '你号啊'
let [a,b,c] = str1
console.log(b) // 号

// 函数解构
var obj = {name:'dmy',age:18}
function a({name,age}){
    console.log(name) // dmy
    console.log(age)  // 18
}
a(obj) // 
```

#### 54.4 箭头函数

```js
/* 
    箭头函数没有 this，所以需要通过查找作用域链来确定 this 的值
    这就意味着如果箭头函数被非箭头函数包含，this 绑定的就是最近一层非箭头函数的 this。
*/

// 例子1 需求：执行 new Button('这里给一个id') 这样就可以将id为这个的按钮绑定一个点击就会改变背景颜色的功能
function Button(id) {
    this.element = document.querySelector("#" + id); // 找到这个元素 赋值给this.element
    this.bindEvent(); // 看下面
}

Button.prototype.bindEvent = function() { // 为构造函数的原型绑定一个bindEvent
    this.element.addEventListener("click", this.setBgColor, false);
    // 为刚才那个按钮元素绑定一个click事件 事件为 this.setBgColor
};

Button.prototype.setBgColor = function() {
    // this.element.style.backgroundColor = '#1abc9c'
    // 这里这么写会出问题 会报错Uncaught TypeError: Cannot read property 'style' of undefined
    // 因为你再bindEvent中 addEvenListener给这个元素绑定的时候 this.setBgcolor的this会指向那个元素 你这里元素.element肯定没用了 因为this就是那个元素了 不需要.element
    this.style.backgroundColor = '#1abc9c' // 这样可以解决
    // 但是！ 确实可以这样做，但是在实际的开发中，我们可能会在 setBgColor 中还调用其他的函数(比如你又在Button的原型上绑了其他的事件 你)
};
var button = new Button("button");

// 解决办法1  Es5 解决
Button.prototype.bindEvent = function() {
    this.element.addEventListener("click", this.setBgColor.bind(this), false);
    // 利用bind(this) 把this直接绑到实例上
};
// 解决办法2 Es6 解决
Button.prototype.bindEvent = function() {
    this.element.addEventListener("click", event => this.setBgColor(event), false);
    // 由于箭头函数没有 this，所以会向外层查找 this 的值，即 bindEvent 中的 this，此时 this 指向实例对象，所以可以正确的调用 this.setBgColor 方法， 而 this.setBgColor 中的 this 也会正确指向实例对象。
};

// 最后，因为箭头函数没有 this，所以也不能用 call()、apply()、bind() 这些方法改变 this 的指向，可以看一个例子：


// 2.箭头函数是没有自己的arguments的 但是它可以访问到外层函数的arguments
function a(b){
    return ()=>arguments[0]
}
let result = a('你好啊')
console.log(result()) // 你好啊

// 如果我们就是要访问箭头函数的实参呢？
// 你可以通过命名参数或者 rest 参数的形式访问参数:
let nums = (...nums) => nums;


// 3. 箭头函数不能通过new调用
// 补充： JavaScript 函数有两个内部方法：[[Call]] 和 [[Construct]]当通过 new 调用函数时，执行 [[Construct]] 方法，创建一个实例对象，然后再执行函数体，将 this 绑定到实例上。
var Foo = () => {};
var foo = new Foo(); // TypeError: Foo is not a constructor


// 4.箭头函数没有new.target
// 看下面例子先了解什么是new.target 其实就是让实例只能通过new的方式来创建 不可以通过call方法这种改变this的方法来创建 new.target 如果不是用new的 那么返回undefined
function Person(name) {
  if (new.target !== undefined) {
    this.name = name;
  } else {
    throw new Error('必须使用 new 命令生成实例');
  }
}

// 另一种写法
function Person(name) {
  if (new.target === Person) {
    this.name = name;
  } else {
    throw new Error('必须使用 new 命令生成实例');
  }
}

var person = new Person('张三'); // 正确
var notAPerson = Person.call(person, '张三');  // 报错

// 箭头函数都不能用new来调用 它有个屁的 new.target

// 5.箭头函数是没有原型的
var Foo = (a,b)=>{
    this.a = a
    this.b = b
}
Foo.prototype  // undefined
```

#### 54.5 Symbol类型

```js
// Symbol 是ES6 新增的一种类型 使用typeof 可以得到 'Symbol'
var s = Symbol()
console.log(typeof s) // Symbol

// Symbol 不会通过new来创建 这是因为生成的 Symbol 是一个原始类型的值，不是对象。

/*
	Symbol 作为属性名，该属性不会出现在 for...in、for...of 循环中，也不会被 Object.keys()、Object.getOwnPropertyNames()、JSON.stringify() 返回。但是，它也不是私有属性，有一个 Object.getOwnPropertySymbols 方法，可以获取指定对象的所有 Symbol 属性名。
*/
var obj = {};
var a = Symbol('a');
var b = Symbol('b');

obj[a] = 'Hello';
obj[b] = 'World';

var objectSymbols = Object.getOwnPropertySymbols(obj);

console.log(objectSymbols);
// [Symbol(a), Symbol(b)]
```

#### 54.6 for of

```js
// 先利用ES5 写一个迭代器
function iteration(item){
    var i = 0 // 设置第一个值的索引为0
    return {
        next:function (){
            var done = i >= item.length // done表示的是 是否还有下一个值 如果没有了就是false
            var value = !done ? item[i++] : undefined // i++ 先做运算再++ 等于你先拿item[i] 然后加
            return {
                value:value,
                done:done
            }
        }
    }
}

// 遍历数组对象
const colors = ["red", "green", "blue"];

for (let color of colors) {
    console.log(color);
}
// red
// green
// blue

// 由此可见 ES6给默认的一些数据结构设置了Symbol.iterator 本质上 for of就是循环对象的Symbol.iterator属性
/** for of 可以循环的数据类型
	   数组
        Set
        Map
        类数组对象，如 arguments 对象、DOM NodeList 对象
        Generator 对象
        字符串
/
```

#### 54.7 Set 和 Map

```js
// 类似于数组 它所包含的值是唯一的 无重复
// set 可以用new来创建
let a = new Set()

// Set 函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。
var arr1 = [1,1,2,3]
var arr2 = new Set(arr1)
console.log(arr2) // [1,2,3]

set = new Set(document.querySelectorAll('div'));
console.log(set.size); // 66

set = new Set(new Set([1, 2, 3, 4]));
console.log(set.size); // 4

/*
	Set的一些操作
	    add(value)：添加某个值，返回 Set 结构本身。
        delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
        has(value)：返回一个布尔值，表示该值是否为 Set 的成员。
        clear()：清除所有成员，无返回值。
*/
// 例子
var arr1 = new Set()
arr1.add(1).add(2)
console.log(arr1) // [1,2]

arr1.delete(1) // true
arr1.delete(3) // false

arr1.has(1) // true
arr1.has(5) // false

arr1.clear  []

// 遍历方法
  var a = new Set([{'a':1},{'b':2}])
  // keys
  console.log(...a.keys()) // {a:1},{b:2}
  // values
  console.log(...a.values()) //   {a:1},{b:2}
  // forEach 参数是一个回调函数 回调函数的参数是 值与key
  let set = new Set([1, 2, 3]);
  set.forEach((value, key) => console.log(key + ': ' + value));



// 利用 Set 对数组去重
let arr = [1,1,2,2,3]
let arr1 = [...new Set(arr)] // new Set(arr) 返回的是 {0:1,1:2,2:3}
console.log(arr1) // [1,2,3] 



// Map 
// Map对比object最大的好处就是，key不受类型限制
// 定义map
const map1 = new Map()
// 新增键值对 使用 set(key, value)
map1.set(true, 1)
map1.set(1, 2)
map1.set('哈哈', '嘻嘻嘻')
console.log(map1) // Map(3) { true => 1, 1 => 2, '哈哈' => '嘻嘻嘻' }
// 判断map是否含有某个key 使用 has(key)
console.log(map1.has('哈哈')) // true
// 获取map中某个key对应的value 使用 get(key)
console.log(map1.get(true)) // 2
// 删除map中某个键值对 使用 delete(key)
map1.delete('哈哈')
console.log(map1) // Map(2) { true => 1, 1 => 2 }

// 定义map，也可传入键值对数组集合
const map2 = new Map([[true, 1], [1, 2], ['哈哈', '嘻嘻嘻']])
console.log(map2) // Map(3) { true => 1, 1 => 2, '哈哈' => '嘻嘻嘻' }
```

#### 54.8 WeakMap

```js
// 学习这个之前 先了解一下强引用与弱引用
/*
在计算机程序设计中，弱引用与强引用相对，是指不能确保其引用的对象不会被垃圾回收器回收的引用。 一个对象若只被弱引用所引用，则被认为是不可访问（或弱可访问）的，并因此可能在任何时刻被回收。
*/

// 强引用 就是我们一般创建一个对象 都是强引用的
var obj = new Object() // 强引用
// 如果你要使它触发垃圾回收
obj = null

// WeakMap 可以让我们不用管创建的对象 它会进行垃圾回收

// 应用1 我们使用Jquery的时候可以使用$.data() 去管理一个元素和它的一些属性数据 那当我们删除这个元素的时候 它的属性数据还是存在内存的
let wm = new WeakMap(), element = document.querySelector(".element");
wm.set(element, "data");
let value = wm.get(elemet);
console.log(value); // data
element.parentNode.removeChild(element);
element = null;
```

#### 54.9 协程Generator

```js
// 先来看看 yield
functionasnycJob(){
    // ...其他代码
    var f=yield readFile( fileA);
    // ...其他代码

}

/*
	上面代码的函数 asyncJob 是一个协程，它的奥妙就在其中的 yield 命令。它表示执行到此处，执行权将交给其他协程。也就是说，yield命令是异步两个阶段的分界线。

协程遇到 yield 命令就暂停，等到执行权返回，再从暂停的地方继续往后执行。它的最大优点，就是代码的写法非常像同步操作，如果去除yield命令，简直一模一样。
*/

// 关于Generator函数 这种函数有一个特点就是函数名字前面有一个星号
  function*gen(x){
  console.log('开始了准备计算y')
  var  y=yield x+2;
  console.log('歇一会')
  var  d=yield x+3;
  console.log('算完d了')
  return '111'
  }
  var g = gen(1)
  console.log(g.next()) // 打印开始准备计算y 然后 遇到第一个yield 返回后面的语句 {value:3,done:false}
  console.log(g.next()) // 打印歇一会 然后遇到第二个yield 返回后面的语句 {value:4,done:true}
  console.log(g.next()) // 打印算完d了 并且后面没有yield了 只有return了所以返回return后面的 {value:'111',done:true}
```

#### 54.10 class

```js
// 之前
var Person = function(name){
    this.name = name
}
Person.prototype.sayname = function(){
    console.log(this.name)
}
var person = Person('james')
person.sayname() // james

// 现在的class
// 1.简单使用
class Person{
    constructor(name){
      this.name = name
    }
    sayName(){
      console.log(this.name)
    }
  }
  var  person = new Person('詹姆斯')
  person.sayName() // 詹姆斯
// 2.静态
class Person{
    constructor(name){
      this.name = name
    }
    static age = 13
	static fun(){
        console.log('只能我用')
    }
    sayName(){
      console.log(this.name)
    }
  }
  Person.age // 13
  Person.fun() // 只能我用
  var person = new Person('詹姆斯')
  person.age // undefined
  person.fun() // fun not a function

// 继承
class Person{
    constructor(name){
      this.name = name
    }
    static age = 13
	static fun(){
        console.log('只能我用')
    }
    sayName(){
      console.log(this.name)
    }
  }
 class Cat extends Person{
     say(){
         console.log(this.name)
     }
 }
var cat1 = new Cat('卡特')
cat1.say() // 卡特
```

#### 54.11 for in  and  for of

```js
let obj = {name:'dmy',age:11}
let arr = [1,2,3,4,5]

for(let key in obj){
    console.log(key)
}
/*
	name
	age
	都是打印的key
*/

for(let key1 in arr){
    console.log(key1)
}
/*
0
1
2
3
4
都是打印的index索引
*/

for(let v of arr){
    console.log(v)
}
/*
1
2
3
4
5
都是打印的值
*/

// 对象除非设置哪个迭代器属性 否则无法使用for of 的
```



### 55 本地存储

```js
// 1.cookies
var cok = '123'
document.cookie = 'token' + '=' + cok

// 2.localStorage和sessionStorage
var name='sessionData';
var num=120;

//存储数据
sessionStorage.setItem(name,num);
sessionStorage.setItem('value2',119);

//获取全部数据
let dataAll=sessionStorage.valueOf();
console.log(dataAll,'获取全部数据');

//获取指定键名数据
var dataSession=sessionStorage.getItem(name);
var dataSession2=sessionStorage.sessionData;//sessionStorage是js对象，也可以使用key的方式来获取值
console.log(dataSession,dataSession2,'获取指定键名数据');

//删除指定键名数据
sessionStorage.removeItem(name);
console.log(dataAll,'获取全部数据1');

//清空缓存数据：localStorage.clear();
sessionStorage.clear();
console.log(dataAll,'获取全部数据2');  

/*
	cookie：可设置失效时间，没有设置的话，默认是关闭浏览器后失效

	localStorage：除非被手动清除，否则将会永久保存。

	sessionStorage： 仅在当前网页会话下有效，关闭页面或浏览器后就会被清除。
*/
/*
	http
		cookie：每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题,每次请求都会携带大量数据所以应该尽可能的不使用，但是在用户登录的需求上比较好用

localStorage和sessionStorage：仅在客户端（即浏览器）中保存，不参与和服务器的通信,sessionStorage只保存当前页面的信息，用于存储一些临时数据以免用户刷新界面就会丢失数据，而localStorage可以跨页面传递数据
*/
```

### 56 async与await

```js
/*
	async 函数是 Generator 函数的语法糖。使用 关键字 async 来表示，在函数内部使用 await 来表示异步。相较于 Generator，async 函数的改进在于下面四点：

内置执行器。Generator 函数的执行必须依靠执行器，而 async 函数自带执行器，调用方式跟普通函数的调用一样

更好的语义。async 和 await 相较于 * 和 yield 更加语义化

更广的适用性。co 模块约定，yield 命令后面只能是 Thunk 函数或 Promise对象。而 async 函数的 await 命令后面则可以是 Promise 或者 原始类型的值（Number，string，boolean，但这时等同于同步操作）

返回值是 Promise。async 函数返回值是 Promise 对象，比 Generator 函数返回的 Iterator 对象方便，可以直接使用 then() 方法进行调用

async 表示函数里有异步操作
await 表示紧跟在后面的表达式需要等待结果。
*/

// 1. 基础使用
  async function abc(){
    return 'hello js'
  }
  console.log(abc())
  /*
  打印
  Promise {<fulfilled>: "hello js"}
    [[Prototype]]: Promise
    [[PromiseState]]: "fulfilled"
    [[PromiseResult]]: "hello js"
  */
// 2. 主动抛错
  async function abc(){
    throw new Error('错误信息是我')
  }
  abc()
  .then(result=>{console.log('成功了'+result)})
  .catch(error=>{console.log('失败了'+error)})

  /*
    打印
    失败了Error: 错误信息是我
    我们看到函数内部抛出了一个异常，返回reject，async函数接收到之后，判定执行失败进入catch，该返回的错误打印了出来。
  */

// return 什么的时候是 resolve 什么时候是 catch呢？
/*
	async函数接收到返回的值，发现不是异常或者reject，则判定成功，这里可以return各种数据类型的值，false,NaN,undefined...总之，都是resolve
但是返回如下结果会使async函数判定失败reject

内部含有直接使用并且未声明的变量或者函数。

内部抛出一个错误throw new Error或者返回reject状态return Promise.reject('执行失败')

函数方法执行出错（🌰：Object使用push()）等等...

还有一点，在async里，必须要将结果return回来，不然的话不管是执行reject还是resolved的值都为undefine，建议使用箭头函数。
其余返回结果都是判定resolved成功执行。

*/

// await
/*
	await意思是async wait(异步等待)。这个关键字只能在使用async定义的函数里面使用。任何async函数都会默认返回promise，并且这个promise解析的值都将会是这个函数的返回值，而async函数必须等到内部所有的 await 命令的 Promise 对象执行完，才会发生状态改变。
	很多人以为await会一直等待之后的表达式执行完之后才会继续执行后面的代码，实际上await是一个让出线程的标志。await后面的函数会先执行一遍(比如await Fn()的Fn ,并非是下一行代码)，然后就会跳出整个async函数来执行后面js栈的代码。等本轮事件循环执行完了之后又会跳回到async函数中等待await****后面表达式的返回值，如果返回值为非promise则继续执行async函数后面的代码，否则将返回的promise放入Promise队列
*/

// 先使用原始的Promise then catch 写一个逐渐加数
  var timetime = function tdc(time){
    return new Promise((resovle)=>{
      return setTimeout(function(){
        return resovle(time+200)
      },time)
    })
  }
  var first = function(time){
    console.log('第一次'+time)
    return timetime(time)
  }
  var two = function(time){
    console.log('第二次'+time)
    return timetime(time)
  }
  var three = function(time){
    console.log('第三次'+time)
    return timetime(time)
  }

  var abc = function (time1) {
    first(time1).then(time2=>two(time2))
    .then(time3=>three(time3))
    .then(res=>{
      console.log('最后一次延迟'+res)
    })
  }
  abc(500)
// 简单说一下流程 给abc函数传入一个500初始时间，运行first(500)这时会去执行哪个timetime(500)这个函数中执行了一个Promise，内部有一个定时器在多少秒之后resolve 当resolve之后abc函数就往后的then走了 then中是可以拿到你第一次first里面执行完resolve(newtime)传入newtime的然后这时候再给到two函数 依此类推


// 用async和await做一个
var abc = function(time) {
    return new Promise((resolve)=>{
      return setTimeout(function() {
        resolve(time+200)
      },time)
    })
  }
  var first = function(time){
    console.log('第一次'+time)
    return abc(time)
  }
  var two = function(time){
    console.log('第二次'+time)
    return abc(time)
  }
  var three = function(time){
    console.log('第三次'+time)
    return abc(time)
  }
  async function timetime() {
    console.log('开始了啊')
    const inittime = 500
    var time1 = await first(inittime)
    console.log('第一次值'+time1)
    var time2 = await two(time1)
    var time3 = await three(time2)
    console.log('最终等待了'+time3)
    return time3
  }
  timetime()
  .then(res=>{
    console.log(res)
  })

// 流程 执行async函数timetime() 设置一个初始的时间500，利用await先执行first(500)这时候就开始等 等到哪个abc函数中的Promise的resolve执行，将resolve(newtime)这个newtime赋值给time1 进行下一个await two依次类推

/*
	`async`里如果有多个await函数的时候，如果其中任一一个抛出异常或者报错了，都会导致函数停止执行，直接`reject`;
怎么处理呢，可以用try/catch，遇到函数的时候，可以将错误抛出，并且继续往下执行。
*/
   var one = async function () {
    try{
      await Promise.reject('错了') // 主动抛出错误 进入catch
      await '错误了'
    }catch(error){
      console.log('有错的')
    }
    // 下面依然正常执行
    await console.log('继续执行了')
    return '成功返回值'
  }
  one()
  .then(res=>console.log('成功'+res))
  .catch(err=>console.log('错误'+err))
```

### 57 ES7常用

#### 57.1 includes

```js
let arr = [1,2,3,NaN]
const db = arr.includes(1) // true

// 看着是不是有点像indexOf 但是还是不一样的
const ad = arr.indexOf(NaN) // -1 找不到
const as = arr.includes(NaN) // true 可以找到
```

#### 57.2 求幂

```js
const num = 3 ** 2 // 9
```

### 58 ES8 常用

#### 58.1 Object.values

```js
var dirs = {name:'dmy',age:11}
const vt = Object.values(dirs)
console.log(vt) // ['dmy',11]
```

#### 58.2 Object.entries

```js
const obj = {
  name: '林三心',
  age: 22,
  gender: '男'
}

const entries = Object.entries(obj)
console.log(entries) 
// [ [ 'name', '林三心' ], [ 'age', 22 ], [ 'gender', '男' ] ]
```

### 59 ES9 常用

#### 59.1   for await of

```js
// 需求 我们希望第一个Promise中的定时器三秒之后执行 然后再执行一个一秒之后执行的Promise 可以用这个 async await
  function first(time) {
    return new Promise((resolve,reject)=>{
      setTimeout(function () {
        console.log('我经历了三秒了')
        resolve(time)
      },time)
    })
  }
  function two(time) {
    return new Promise((resolve,reject)=>{
      setTimeout(function () {
        console.log('我经历了1秒')
        resolve(time)
      },time)
    })
  }
  async function fn() {
    let time1 = await first(3000)
    let time2 = await two(2000)
    return '完毕'
  }
  fn().then(res=>{
    console.log(res)
  })
  // 但是 如果我们有一百个await 这种东西 需要写一百次 怎么解决呢？
  function fn (time) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${time}毫秒后我成功啦！！！`)
    }, time)
  })
}

async function asyncFn () {
  const arr = [fn(3000), fn(1000), fn(1000), fn(2000), fn(500)]
  for await (let x of arr) {
    console.log(x)
  }
}

asyncFn()
/*
  3000毫秒后我成功啦！！！
  1000毫秒后我成功啦！！！
  1000毫秒后我成功啦！！！
  2000毫秒后我成功啦！！！
  500毫秒后我成功啦！！！
*/
```

### 60 fetch

```js
/*
	Fetch API 提供了一种全局fetch()方法，该方法位于 WorkerOrGlobalScope 这一个 mixin 中 方法用于发起获取资源的请求。它返回一个 promise，这个 promise 会在请求响应后被 resolve，并传回 Response 对象。
*/
fetch(url,options).then((response)=>{
    // 处理 请求过来的数据
},(error)=>{
    // 处理错误
})
/*
	options 参数可选项
	method: 请求使用的方法，如 GET、POST。
    headers: 请求的头信息，包含与请求关联的Headers对象。
    body: 请求的 body 信息。注意 GET 或 HEAD 方法的请求不能包含 body 信息
    mode: 请求的模式，如 cors、 no-cors 或者 same-origin。
    credentials: 请求的 credentials，如 omit、same-origin 或者 include。为了在当前域名内自动发送 cookie 必须提供这个选项。
*/

// 案例1 对于表单数据用POST提交
function postForm() {
  const form = document.querySelector('form')
  const name = encodeURI(document.getElementsByName('name')[0].value)
  fetch(`/api/user/${name}`, {
    method: 'POST',
    body: new FormData(form)
  })
}

// 对于什么时候返回这个 reject 404是不会走reject的 会走resolve 只有网络请求才可以触发reject
```

### 61 axios

#### 61.1 安装与简单使用

```js
// 2.使用
/* Get请求 */
axios.get('/url?Id=1')
.then((res)=>{
    
}).catch(err=>{
    
})
// 上面那种带参数也可以改成这样
axios.get('/url',{
    params:{
        Id:1
    }
})
.then((res)=>{
    
}).catch(err=>{
    
})

/* POST请求 */
axios.get('/url',{
    firstName: 'ddd',
    lastName: 'aaa'
})
.then((res)=>{
    
}).catch(err=>{
    
})

/* 多个请求 */
function getUserAccount() {
    return axios.get('/user/12345');
}

function getUserPermissions() {
    return axios.get('/user/12345/permissions');
}

axios.all([getUserAccount(), getUserPermissions()])
    .then(axios.spread(function (acct, perms) {
    // 两个请求现在都执行完成
}));

// 我们也可以自己传递一些config配置
axios({
    method: 'POST',
    url: '/abc/ddd',
    data:{
            firstName: 'ddd',
    		lastName: 'aaa'
    }
})
```

#### 61.2 自定义一个实例

```js
// 自定义配置创建一个axios实例
var instance = axios.create([options])
/*
	options参数
	 // `url` 是用于请求的服务器 URL
    url: '/user',

    // `method` 是创建请求时使用的方法
    method: 'get', // 默认是 get

    // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
    // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
    baseURL: 'https://some-domain.com/api/',

    // `headers` 是即将被发送的自定义请求头
    headers: {'X-Requested-With': 'XMLHttpRequest'},

    // `params` 是即将与请求一起发送的 URL 参数
    // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
    params: {
      ID: 12345
    },

    // `paramsSerializer` 是一个负责 `params` 序列化的函数
    // (e.g. https://www.npmjs.com/package/qs,       
    http://api.jquery.com/jquery.param/)
      paramsSerializer: function(params) {
      return Qs.stringify(params, {arrayFormat: 'brackets'})
    },

    // `data` 是作为请求主体被发送的数据
    // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
    // 在没有设置 `transformRequest` 时，必须是以下类型之一：
    // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
    // - 浏览器专属：FormData, File, Blob
    // - Node 专属： Stream
    data: {
      firstName: 'Fred'
    },

      // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
      // 如果请求花费了超过 `timeout` 的时间，请求将被中断
      timeout: 1000,

      // `withCredentials` 表示跨域请求时是否需要使用凭证
      withCredentials: false, // 默认的

      // `adapter` 允许自定义处理请求，以使测试更轻松
      // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs]      
     (#response-api)).
    adapter: function (config) {
      /* ... */
    },

    // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
    // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置      
    的自定义 `Authorization`头
    auth: {
      username: 'janedoe',
      password: 's00pers3cret'
    },

    // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob',         
   'document', 'json', 'text', 'stream'
   responseType: 'json', // 默认的

   // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` 是承载 xsrf token 的值的 HTTP 头的名称
  xsrfHeaderName: 'X-XSRF-TOKEN', // 默认的

    // `onUploadProgress` 允许为上传处理进度事件
    onUploadProgress: function (progressEvent) {
      // 对原生进度事件的处理
    },

    // `onDownloadProgress` 允许为下载处理进度事件
    onDownloadProgress: function (progressEvent) {
      // 对原生进度事件的处理
    },

    // `maxContentLength` 定义允许的响应内容的最大尺寸
    maxContentLength: 2000,

    // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject      promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
    validateStatus: function (status) {
    return status >= 200 && status < 300; // 默认的
    },

    // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
    // 如果设置为0，将不会 follow 任何重定向
    maxRedirects: 5, // 默认的

    // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和       
    https 时使用的自定义代理。允许像这样配置选项：
    // `keepAlive` 默认没有启用
    httpAgent: new http.Agent({ keepAlive: true }),
    httpsAgent: new https.Agent({ keepAlive: true }),

    // 'proxy' 定义代理服务器的主机名称和端口
    // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
    // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用   
    `header` 设置的自定义 `Proxy-Authorization` 头。
    proxy: {
      host: '127.0.0.1',
      port: 9000,
      auth: : {
        username: 'mikeymike',
        password: 'rapunz3l'
      }
    },

    // `cancelToken` 指定用于取消请求的 cancel token
    // （查看后面的 Cancellation 这节了解更多）
    cancelToken: new CancelToken(function (cancel) {
    })
  }  
```

#### 61.3 拦截器

```js
// 简单来说作用就是在.then或者.catch 之前拦截它们做一些操作

// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
}, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
});

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
}, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
});

// 去除拦截器
 var myInterceptor = axios.interceptors.request.use(function () {/*...*/});
 axios.interceptors.request.eject(myInterceptor);

// 对于自定义的实例怎么添加拦截器？
var instance = axios.create([options])
instance.interceptors.request.user(...)
```

#### 61.4 使用validateStatus 配置来检验状态码

```js
axios.get('/url',{
    validateStatus:function(status){
        return status < 500;
    }
})
```

#### 61.5 注意

```js
// 对于后端必须以application/x-www-form-urlencoded这也的形式，那么我们需要对data进行序列化不能以json的格式应该以键值对的形式来进行传值

// 方式1
// user.js
import myAxios from './axios';

export function loginAPI(paramsList) {
  return myAxios({
    url: '/api/login',
    method: 'post',
    data: paramsList,
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
    },
    transformRequest: [
      (data) => {
        let result = ''
        for (let key in data) {
          result += encodeURIComponent(key) + '=' + encodeURIComponent(data[key]) + '&'
        }
        return result.slice(0, result.length - 1)
      }
    ],
  });
}

// 使用qs模块进行序列化
npm install qs
// user.js
import qs from 'qs';
export function loginAPI(paramsList) {
  return myAxios({
    url: '/api/login',
    method: 'post',
    data: paramsList,
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
    },
    transformRequest: [
      (data) => {
        return qs.stringify(data)
      }
    ],
  });
}
```

#### 61.6 对于重复的请求

```js
// 在开发过程中我们应该对一个按钮这种进行一个控制 以免多次发送请求，比如订单的生成如果不进行控制那么它生成两个订单就坏了所以我们可以对请求进行去重利用Map这种 但是其实真正开发前端和后端也都会进行控制
// 开始
var CancelToken = axios.CancelToken;
var cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  })
});

// 取消请求
cancel();
/*
	简单理解就是通过 new axios.CancelToken()给每个请求带上一个专属的CancelToken，之后会接收到一个cancel() 取消方法，用于后续的取消动作，所以我们需要对应的存储好这个方法。
*/



/* 正片 */
// axios.js
const pendingMap = new Map(); // 创建一个Map对象

/* 获取唯一Key的方法 */
function getPendingKey(config) {
  let {url, method, params, data} = config;
  if(typeof data === 'string') data = JSON.parse(data); // response里面返回的config.data是个字符串对象
  return [url, method, JSON.stringify(params), JSON.stringify(data)].join('&');
}


function addPending(config) {
  const pendingKey = getPendingKey(config);
  config.cancelToken = config.cancelToken || new axios.CancelToken((cancel) => {
    if (!pendingMap.has(pendingKey)) {
      pendingMap.set(pendingKey, cancel);
    }
  });
}
```

