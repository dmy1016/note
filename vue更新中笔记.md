# Vue

下载

NPM使用 不用CDN和下载

```

```

代码规范

一般都用两个空格的缩进

## 1.使用

### 1.1初体验

```web-idl
// Vue 是声明式编程
1. 初体验
<div id="app">{{message}}</div>
<script src="../vue.min.js"></script>
<script>
    // 定义变量  let(变量，可修改)/const(常量，不可以修改)
    const app = new Vue({
        el:'#app', // 管理哪个区域
        data:{ // 定义数据
            message:'Vue hello'
        }
    })
</script>

2.列表展示
<div id="app">
  <ul>
    <li v-for="items in message">{{items}}</li>
    <!-- v-for:"element in 定义的可循环对象"-->
  </ul>
</div>
<script src="../vue.min.js"></script>
<script>
  // 定义变量  let(变量，可修改)/const(常量，不可以修改)
  const app = new Vue({
    el:'#app', // 管理哪个区域
    data:{ // 定义数据
      message:['1','2','3']
    }
  })


3.计数器
<div id="app">
    <h1>当前记数:{{counter}}</h1>
    <!--第一种方法 v-on不适合-->
    <!--    <button v-on:click="counter++">+</button>-->
    <!--    <button v-on:click="counter&#45;&#45;">-</button>-->
    <!--第二种方法-->
    <!-- v-on:(监听什么事件)="函数名称" -->
    <button v-on:click="add">+</button>
    <button v-on:click="sub">-</button>
</div>
<script src="../vue.min.js"></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            'counter': 0
        },
        methods: {
            // methods 里面可以定义多个函数
            add: function () {
                this.counter++
            },
            sub: function () {
                this.counter--
            },
        }
    })
</script>
```

### 1.2 模板的设置

首先写好一段代码

```js
<div id="app">
	{{message}}
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		}
	})
</script>
// 找到settings中 Live Templates 找到vue 把这个加进去 下面哪个Default 也要指定一下Html
```

### 1.3 v-once 和 v-html 的使用

```html
<div id="app">
	<h1>{{message}}</h1>
	<h1 v-once>{{message}}</h1>
	<!-- v-one 的作用是 不绑定了 改了data中的值这里也不会改 -->
	<h1 v-html="url"></h1>
	<!-- v-html 可以解析标签的数据	-->
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:'123',
			url:'<a href="https://www.baidu.com">百度一下</a>'
		}
	})
</script>
```

### 1.4 v-cloak的使用

```html
<div id="app" v-cloak>
  <!-- 如果js代码卡住了 那么就无法解析这个message数据了 这时候会很难看 所以加一个v-cloak 然后给它加一个样式 在没解析出来之前先隐藏起来 -->
	{{message}}
</div>
<script src="../vue.min.js"></script>
<script>
  setTimeout(function () {
    const app = new Vue({
      el:'#app',
      data:{
        message:'你好啊'
      }
    })
  },1000)
```

### 1.5 v-bind的使用

```html
<!-- -->
<!-- 1.对于v-bind绑定数据 -->
<body>
<div id="app">
	<img v-bind:src="url" alt="">
	<!-- v-bind:src=“” 或者 v-bind:href=“” 等等 可以绑定数据 就不用写死了	-->
	<!-- 第二种 语法糖	-->
	<img :src="url" alt="">
	<!-- 只用一个:	-->
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:'',
			url:'https://cn.vuejs.org/images/logo.png'
		}
	})
</script>
</body>



<!-- 2.对于v-bind绑定class -->
<!-- v-bind:class="这里面不仅可以传一个对象{} 还可以传入一个数组['class1','class2'] 或者 [class1,class2]这种就是变量的形式会从data中拿 还有一个就是函数 v-bind:class="getclass() 你可以在 下面的methods中写一个函数 返回一个对象或者一个数组都可以 但是函数最后要加括号" -->
<body>
<div id="app">
  <!-- v-bind:class="{}" 这里可以传入一个对象 为true的时候则加上这个class 为false 就不会弄到这个class中  -->
	<h1 v-bind:class="{active:isActive,line:isLine}">你好啊</h1>
  <button v-on:click="alertclass">点击</button>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:'',
      isActive:true,
      isLine:true,
		},
    methods:{
		  alertclass:function () {
		    // if (this.isActive == true){
        //   this.isActive = false
        // }else {
		    //   this.isActive = true
        // }
        this.isActive = !this.isActive
      }
    }
	})
</script>
</body>

<!-- 3.对于style 的绑定 -->
<body>
<div id="app">
  <!-- 绑定style 的时候 对象中的key可以使用驼峰命名 value 必须加引号否则会报错 它会以为是一个变量去data中找 -->
	<h1 :style="{fontSize:'50px'}">你好啊</h1>
  <!-- 补充不写了就：它也可以传入一个methods 或者一个数组 数组中是一个变量[BaseStyle] 这个BaseStyle 写入这个data中是一个字典 -->
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		}
	})
</script>
</body>


例子
<!-- 绑定一个 attribute -->
<img v-bind:src="imageSrc">

<!-- 动态 attribute 名 (2.6.0+) -->
<button v-bind:[key]="value"></button>

<!-- 缩写 -->
<img :src="imageSrc">

<!-- 动态 attribute 名缩写 (2.6.0+) -->
<button :[key]="value"></button>

<!-- 内联字符串拼接 -->
<img :src="'/path/to/images/' + fileName">

<!-- class 绑定 -->
<div :class="{ red: isRed }"></div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]">

<!-- style 绑定 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>

<!-- 绑定一个全是 attribute 的对象 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>

<!-- 通过 prop 修饰符绑定 DOM attribute -->
<div v-bind:text-content.prop="text"></div>

<!-- prop 绑定。“prop”必须在 my-component 中声明。-->
<my-component :prop="someThing"></my-component>

<!-- 通过 $props 将父组件的 props 一起传给子组件 -->
<child-component v-bind="$props"></child-component>

<!-- XLink -->
<svg><a :xlink:special="foo"></a></svg>
```

### 1.6 小作业

```html
<!-- 具体实现 一个有序列表 第一个是红色  剩下点哪个 哪个就红色 -->
<body>
<div id="app">
	<ul>
    <li v-for="(item,index) in moves" v-bind:class="{active:currentIndex===index}" v-on:click="getclasses(index)">{{item}}</li>
  </ul>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
		    moves:['喜羊羊','美羊羊','肥羊羊','灰羊羊'],
      		currentIndex:0
		},
    methods:{
      getclasses:function (index) {
        this.currentIndex = index
      }
    }
	})
</script>
</body>
<!--
流程：
	在Vue JS 代码中定一个0 就是currentIndex 如果是第一个那么就是true class 就是active
	再监听一个点击事件传入index 参数 点哪个就改一下currentIndex 为当前点的这个index
-->
```

### 1.7 计算属性

计算属性多次使用只会调用一次 因为有缓存

#### 1.7.1 常用

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<h1>{{fullName}}</h1>

</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			firstName:'Lebron',
			lastName:'James',
		},
	 	// 计算属性computed 通常不要用动词开头 像get这一类的
		computed:{
			fullName:function () {
				return (this.firstName + this.lastName)
			}
		}
	})
</script>
</body>
</html>
```

#### 1.7.2 本质

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<h1>{{fullName}}</h1>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			firstName:'Kobye',
			lastName: 'Bylant',
		},
		computed:{
			// 一般来说 我们只是实现get方法即可
			fullName:{
				set:function (newValue){
					const name = newValue.split(' ')
					this.firstName = name[0]
					this.lastName = name[1]
					console.log(name)
				},
				get:function (){
					return this.firstName + this.lastName
				}
			}
			// 底下是简便写法
			// fullName:function (){
			// 	return this.firstName + this.lastName
			// }
		}
	})
</script>
</body>
</html>
```

#### 1.7.3 methods 和 计算属性对比

尽量使用计算属性 因为它内部是有一个缓存 methods 不会缓存你的数据 如果多个数据都一样的话 那么vue内部就不会调用了 只调用第一次 然后后面因为都一样所以直接从缓存拿

### 1.8 es6语法

#### 1.8.1 var/let

```html
1. var 可以说是 js中比较失败的 因为它在for 和 if 中是没有作用域的 也就是 无法是私有变量 哪都能改
2. 函数是有作用域的
```

#### 1.8.2 const

```javascript
1.将变量修饰成一个常量
const a = 1
a = 2  // 这样会报错
2. const 内存地址不能改变
const 
// 一旦设置一个值 那么它的内存地址是无法改变的 let就不一样可以修改
3.const 定义一个对象里面的属性是可以变得
<script>
  const kobe = {
    name:'kobe',
    age:'11'
  }
  kobe.name = 'dmy'
  kobe.age = '11'
</script>
```

### 1.9 v-on（事件监听）

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<h1>{{counter}}</h1>
  <!--  1.非语法糖  -->
<!--  <button v-on:click="increament">+</button>-->
<!--  <button v-on:click="decreament">-</button>-->
  <!--  2.语法糖  -->
<!--    <button @click="increament">+</button>-->
<!--    <button @click="decreament">-</button>-->
  <!--  3.带参数  -->
<button @click="innerjob('你好啊')"></button>
  <!--  4.methods中要求有参数但是没带 那么vue就会默认将浏览器生成的事件当做参数传递进去  -->
<button @click="noinnser"></button>
  <!--  5.如何传递两个 一个值，一个浏览器默认事件  -->
  <!-- $event 默认就是获取浏览器的事件 -->
<button @click="twoinnerjob(123,$event)"></button>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			counter:0
		},
    methods:{
    //   increament(){
    //     this.counter++
    //   },
    //   decreament(){
    //     this.counter--
    //   }
      innerjob(name){
        console.log(name)
      },
      noinnser(value){
        // 如果 v-on:click="noinnser" 这样写 那么就会将浏览器默认生成的事件当做参数传递进去
        // 如果 v-on:click="noinnser()" 这样写只加了括号 这样打印出来就是 undefined
        console.log(value)
      },
      twoinnerjob(value,event){
        console.log(value,event)
      }
    }
	})
</script>
</body>
</html>
```

### 1.10 v-on 修饰符的使用

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<!-- 	@click.stop修饰符 -->
	<div @click="btndiv">
		aaaaaaaaaaaaa
	<!--	如何组织冒泡呢 就是@click.stop	-->
		<h1 @click.stop="btnh1">点击</h1>
	</div>
	<!--	@click.prevent修饰符  -->
	<form action="baidu">
	<!--	这里是默认会提交过去 如何组织默认事件呢？	 -->
	<!--	加入@click.prenent 就组织了默认的提交	-->
		<input type="submit" value="提交" @click.prevent="preventindent">
	</form>
	<!--	@keyup.enter修饰符  -->
	<form>
	<!--	键帽抬起事件 如何做到监听某一个案件呢 比如enter @keyup.enter	-->
		<input type="text" @keyup.enter="keyupup">
	</form>
	<!-- @click.once修饰符	-->
	<!-- 按钮事件只监听一次	-->
	<button @click.once="btn2click">按钮2</button>
    
    <!--  @keydown.native	-->
    <!--  vue中的语法糖会绑定某一个按键比如keydown.enter 但是如果需求是需要按一下监听很多按键那么你需要使用@keydown.native="事件" 事件中接受一个event 这个event就是js原生的键盘事件 因为vue中的keydown和js原生的重名了 所以有这种需求要这么写	-->
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
		methods:{
			btndiv(){
				console.log('btndiv')
			},
			btnh1(){
				console.log('btnh1')
			},
			preventindent(){
				console.log('阻止了')
			},
			keyupup(){
				console.log('我抬起来了？？？')
			},
			btn2click(){
				console.log('我发生了一次')
			}
		}
	})
</script>
</body>
</html>
```

### 1.11 判断事件

#### 1.11.1 v-if

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<h1 v-if="isShow">
  <!--   v-if 中为一个boolean值  -->
    {{message}}
  </h1>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:'你好啊',
      isShow:true
		}
	})
</script>
</body>
</html>
```

#### 1.11.2 v-if和v-else

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <h1 v-if="isShow">
    <!--   v-if 中为一个boolean值  -->
    {{message}}
  </h1>
  <h2 v-else>{{velse}}</h2>
</div>
<script src="../vue.min.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      message:'你好啊',
      velse:'v-if为false时，显示我吧',
      isShow:true
    }
  })
</script>
</body>
</html>
```

#### 1.11.3 用户登录小案例

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <span v-if="isShow">{{text}}</span><span v-else>{{text2}}</span>
  <input type="text" placeholder="用户登录" v-if="isShow"><input type="text" placeholder="邮箱登录" v-else>
  <button @click="convert">切换类型</button>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
		  isShow:true,
			text:'用户登录',
      text2:'邮箱登录'
		},
    methods:{
      convert(){
        this.isShow = !this.isShow
      }
    }
	})
</script>

</body>
</html>
```

#### 1.11.4 登录案例的问题

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<!-- 问题就是vue内部会觉得你这两个显示是互斥的所以它不会生成新的span和input而是改你之前那个 -->
<!-- 怎么解决呢 使用一个key 这样它就不会复用之前的元素了 而是新生成一个元素 -->
<div id="app">
  <div v-if="isShow" key="x1">
    <span >{{text}}</span>
    <input type="text" placeholder="用户登录">
  </div>
  <div v-else key="x2">
    <span >{{text2}}</span>
    <input type="text" placeholder="邮箱登录" >
  </div>
  <button @click="convert">切换类型</button>
</div>
<script src="../vue.min.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      isShow:true,
      text:'用户登录',
      text2:'邮箱登录'
    },
    methods:{
      convert(){
        this.isShow = !this.isShow
      }
    }
  })
</script>
</body>
</html>
```

#### 1.11.5 v-show

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <!-- v-if 如果条件为false则不会显示这个元素了  -->
  <!-- v-show 如果条件为false则会给元素添加一个行内样式 display:none  -->
	<h1 v-if="isShow">{{message}}</h1>
	<h2 v-show="isShow">{{message}}</h2>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
		  isShow:true,
			message:'你好啊'
		}
	})
</script>
</body>
</html>
```

### 1.12 循环遍历

#### 1.12.1 v-for 循环数组

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <!-- 遍历数组  -->
	<ul>
    <li v-for="item in name">{{item}}</li>
  </ul>
  <!-- 遍历数组,拿到key和value  -->
  <ul>
    <li v-for="(item,key) in name">{{key}}-{{item}}</li>
  </ul>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			name:['蜘蛛侠','蝙蝠侠','钢铁侠','美国队长']
		}
	})
</script>
</body>
</html>
```

#### 1.12.2 v-for 循环对象

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <!-- 遍历对象  -->
	<ul>
    <li v-for="value in info">{{value}}</li>
  </ul>
  <!-- 遍历对象,拿到属性和value  -->
  <ul>
    <li v-for="(value,key) in info">{{key}} - {{value}}</li>
  </ul>
	<!-- 遍历对象,拿到属性和value，index  -->
	<ul>
		<li v-for="(value,key,index) in info">{{index}} - {{key}} - {{value}}</li>
	</ul>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			info:{
			  name:'james',
        age:18,
        height:1.88
      }
		}
	})
</script>
</body>
</html>
```

#### 1.12.3 v-for 往中间插值（diff算法）

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<ul>
    <li v-for="item in word" :key="item">{{item}}</li>
  </ul>
</div>
<script src="../vue.min.js"></script>
<script>
  // app.word.splice(2,0,'F')  第一个参数 往哪个位置插入 第二个参数 是否要删除元素 这里为0就是不删除 第三个插入哪个值
  // 这个案例想说明 我们在插入的时候 应该定义一个key 因为这样才会利用diff算法 很节省性能 如果不使用的话它会直接将所有的元素往后移 很笨很慢
	const app = new Vue({
		el:'#app',
		data:{
			word:['A','B','C','D']
		}
	})
</script>
</body>
</html>
```

#### 1.12.4 响应式数据

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <ul>
    <li v-for="item in word">{{item}}</li>
  </ul>
  <button @click="converdata">按钮</button>
</div>
<script src="../vue.min.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      word:['A','B','C','D']
    },
    methods:{
      converdata(){
        // 1.push 往最后插 可以插入一个 也可以插入多个
        // this.word.push('E','F','G')

        // 2.pop 删除最后一个元素
        // this.word.pop()

        // 3.shift 删除第一个元素
        // this.word.shift()

        // 4.unshift 往第一个添加 也可以添加多个
        // this.word.unshift('1','2')

        // 5.splice 的使用  这个函数比较不好记它可以 删除元素/增加元素/替换元素
        // splice(start,删除几个,替换为什么)
        // this.word.splice(1,1)  从第一个开始删除一个
        // this.word.splice(1) 从第一个开始删除后面所有
        // this.word.splice(1,0,'我是插进来的','还有我呢') 从第一个开始删除0个插入两个元素

        // 6.sort 排序
        // this.word.sort()

        // 7.reverse(0
        // this.word.reverse()

        // 8 Vue.set(对象，索引值，修改后的值)
        // Vue.set(this.word,0,'我使用Vue.set改的')

        // 不响应的方式
        // this.word[0] = '改的' 这样不会渲染到页面上
      }
    }
  })
</script>
</body>
</html>
```

### 1.13 购物车小案例

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
  <style>
    .active {
      display: none;
    }
    .xianshi{
      display: none;
    }
  </style>
</head>
<body>
<div id="app">
  <div :class="{active:this.books.length === 0} ">
  <table>
    <tr>
      <th>编号</th>
      <th>书籍名称</th>
      <th>价格</th>
      <th>购买数量</th>
      <th>操作</th>
    </tr>
    <tr v-for="(item,index) in books">
      <td>{{index}}</td>
      <td>{{item.name}}</td>
      <td>{{item.price}}</td>
      <td>
        <button @click="sub(index)">-</button>
        {{item.num}}
        <button @click="add(index)">+</button>
      </td>
      <td><button @click="remove(index)">移除</button></td>
    </tr>
  </table>
    <span>总价格{{fullprice}}</span>
  </div>
  <div :class="{xianshi:this.books.length !== 0}">
    <span>没有了下次再来吧 宝贝</span>
  </div>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
      isShow:false,
			"books":[{
			  'name':'算法导论',
			  'time':'2006-2',
			  'price':59,
        'num':1
      },{
        'name':'Linux',
        'time':'2006-3',
        'price':111,
        'num':1
      },{
        'name':'编程珠玑',
        'time':'2002-2',
        'price':444,
        'num':1
      }]
		},
    methods:{
		  add(index){
		    this.books[index].num += 1
      },
      sub(index){
		    if (this.books[index].num === 0){
          this.books[index].num = 0
        }else {
		      this.books[index].num -= 1
        }

      },
      remove(index){
		    this.books.splice(index,1)
      }
    },
    computed:{
      // fullprice(){
      //   return this.books[0].price
      // }
		  fullprice(){
		    fullprice=0
		    for (let i=0;i<this.books.length;i++){
          fullprice += this.books[i].price * this.books[i].num
        }
		    return fullprice
      }
    }
	})
</script>
</body>
</html>
```

#### 1.14 过滤器

```javascript
1. 实现将86 转换为 ￥86.00
conset app = new Vue({
	el:"#app",
	filters:{
		showPrice(price){
            return '￥' + price.toFixed(2)
            // 这里运用了保留两位小数的函数 toFixed(保留几位)
        }		
	}
})

2. 运用
{{price | 过滤器}}

3. 实战
{{price | showPrice}} // 这样就过滤好了
```

### 1.14 v-model

#### 1.14.1 初识 

```php+HTML
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <input type="text" v-model="message">
	{{message}}
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		}
	})
</script>
</body>
</html>
```

#### 1.14.2 radio的使用

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <label for="man">
    <input type="radio" id="man" v-model="sex" value="男">男
  </label>
  <label for="famel">
    <input type="radio" id="famel" v-model="sex" value="女">女
  </label>
  <div>你选择的是{{sex}}</div>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			"sex":'男'
		}
	})
// 男女是互斥的 在没有学这个v-model之前应该用 name 来进行互斥 就是俩name是一样的 这样就会互斥
// 学过之后 只要用这个v-model='sex' 就能实现互斥
// 默认值："sex":'男' 它也会对应选中 radio
</script>
</body>
</html>
```

#### 1.14.3 label for的好处

不管是单选还是复选框 点击那个文字就能进入到输入状态 或者如果是单选或者多选都会直接选中比较方便

#### 1.14.4 checkbox

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <!-- 单选框 绑定的是一个布尔值-->
  <label for="agree">
    <input type="checkbox" id="agree" v-model="isAgree">同意协议
  <!--  刚开始为false 默认是不会选中的 选中之后 isAgree会变成true  -->
  </label>
  <button :disabled="isAgree">下一步</button>

  <!-- 多选框 绑定的是一个数组-->
  <input type="checkbox" value="篮球" v-model="hobbies">篮球
  <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
  <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
  <input type="checkbox" value="电竞" v-model="hobbies">电竞
  <input type="checkbox" value="手球" v-model="hobbies">手球

  <h1>您的爱好是 {{hobbies}}</h1>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
      isAgree:false,
			message:'',
      hobbies:[]
		}
	})
</script>
</body>
</html>
```

#### 1.14.5 select

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <!-- 单选select 绑定一个列表-->
  <select name="furit" v-model="furit">
    <option value="你">你</option>
    <option value="好">好</option>
    <option value="啊">啊</option>
    <option value="我">我</option>
  </select>
  <div>你选择的是 {{furit}}</div>

  <!-- 多选select 绑定一个列表-->
  <select name="furit" v-model="furits" multiple>
    <option value="你">你</option>
    <option value="好">好</option>
    <option value="啊">啊</option>
    <option value="我">我</option>
  </select>
  <div>你选择的是 {{furits}}</div>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:'',
      furit:[],
      furits:[]
		}
	})
</script>
</body>
</html>
```

#### 1.14.6 值绑定

一般值是不能写死的 要从后台发送过来

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <!-- 以前写的是直接写死的 服务器会动态给一个列表所以这里不能写死 -->
  <label v-for="item in orihobbies" :for="item">
    <input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
  </label>
  您的爱好是 {{hobbies}}
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:'',
      hobbies:[],
      orihobbies:['篮球','羽毛球','曲棍球','lol']
		}
	})
</script>
</body>
</html>
```

#### 1.14.7 三种修饰符

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <!-- 1.lazy  -->
  <!--  v-model.lazy 是懒加载 就是在输入之后失去焦点或者按下回车才会改变message的值 -->
  <label for="text">
    <input type="text" id="text" v-model.lazy="message">
  </label>
  <div>信息是:{{message}}</div>


  <!-- 2.number  -->
  <!-- 用于限制用户只能输入数字  -->
  <label for="number">
    <input type="text" id="number" v-model.number="num">
  </label>
  <div>{{num}}-{{typeof num}}</div>
  <!-- 小知识点：typeof 的使用 后面加你想要知道的类型的值 就会返回一个类型 -->

  <!-- 3.trim  -->
  <!-- 用于去除空格  -->
  <label for="name">
    <input type="text" id="name" v-model.trim="name">
  </label>
  <div>信息是:{{name}}</div>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:'你好啊',
      num:'',
      name:''
		}
	})
</script>
</body>
</html>
```

#### 1.14.8 v-model 原理

```
https://www.jianshu.com/p/2012c26b6933
```



### 1.15 vue 的property

```js
1.vm.$data
// 获取到所有vue实例中的data数据
2.vm.$props
// 当使用父向子传值时 在子组件中 可以打印vm.$props 可以得到子组件中props的值
3.vm.$el
// 可以打印根 如果时子组件则打印template为根底下的元素 如果时父组件那么就是挂app下面的
4.vm.$parent
// 在每个 new Vue 实例的子组件中，其根实例可以通过 $root property 进行访问。
5.vm.$root
// 打印根dom的信息 如果你就是root 那么就是打印你自己
6.vm.$slots
// 打印所有的插槽信息 如果你没有在组件中使用则不显示
7.vm.$refs
// 如果给一个普通的dom使用 那么打印就是这个标签 如果在使用组件的时候使用 看下面
<cpn ref='dom1'></cpn>
// 这样设置了之后 在父组件的方法中打印 this.$refs.dom1.子组件中设置的值
// 应用场景 父调子中的方法
this.$refs.dom1.子类中的方法(传值) // 这个可以在父组件中定义然后触发
8.vm.$attrs
// 当组件层数较多 并且希望父组件穿给重孙组件这种情况 一般做法就是通过props一点点往下面传 但是会让代码变得非常冗余 因为有的地方是没有用到的 所以使用$attrs
// 举例 如果有 父 子 孙这种 那么子组件在用孙组件的时候，需要给子组件绑定v-bind="$attrs",并且在定义孙组件props时必须必定义和父组件中数据一样的名字去接受父组件的数据
9.$watch
this.$watch('你要监听的值',callback函数,{配置比如deep和immediate 这种})
// 你可以将这个写在一些生命周期中 这里写完就是加了watch了
// immediate 默认false false:第一次绑定时不进行监听 true:第一次绑定的时候就会触发handler
// deep 默认为false 如果设置为true则开启深度监听 比如你想监听一个对象里面属性的变化如果不设置深度监听是不管用的
10 $on
用于兄弟组件的传值 具体看这个文档吧
https://www.dxel.cn/901.html
```

### 1.16 inject 注入的使用

```js
// 虽然我们已经有了 $parent 但是如果层级比较多那么很恐怖所以这里使用注入的方式 意思就是子组件很容易就能访问到 父组件中的方法 不用一直找
// 举例

// 父组件中一个方法 并且写一个provide
methods:{
    abc(){
        console.log('注入完毕')
    }
}
provide:function(){
    return {
        abc:this.abc
        // 这里返回一个injects这个变量对应你自己定义的injects函数
    }
}

// 子组件中
inject:["abc"] // 选择注入哪些父的方法

// 子组件直接使用不用再调用 $parent这种
this.abc() // 这样就调用了
```

### 1.17 is的使用（大多用于动态）

```js
// 绑定is
  <body>
    <div id="dynamic-component-demo" class="demo">
      <button
        v-for="tab in tabs"
        v-bind:key="tab.name"
        v-bind:class="['tab-button', { active: currentTab.name === tab.name }]"
        v-on:click="currentTab = tab"
      >
        {{ tab.name }}
      </button>

      <component v-bind:is="currentTab.component" class="tab"></component>
    </div>

    <script>
      // 搞三个组件 放到元组tabs中
      var tabs = [
        {
          name: "Home",
          component: {
            template: "<div>Home component</div>"
          }
        },
        {
          name: "Posts",
          component: {
            template: "<div>Posts component</div>"
          }
        },
        {
          name: "Archive",
          component: {
            template: "<div>Archive component</div>"
          }
        }
      ];

      new Vue({
        el: "#dynamic-component-demo",
        data: {
          // 将上面定义的tabs放到Vue实例中
          tabs: tabs,
          // currentTab默认为元组的第一个
          currentTab: tabs[0]
          // 当点击按钮时 会切换currentTab的值 从而导致绑定is变化 实现组件的切换
        }
      });
    </script>
  </body>
</html>

// 诸如 html中的 ul  li select 这样的 里面的内容标签是要严格按照要求的，这样大大的限制了我们的编写 这个is就帮到了我们
<table>
    <tr :is="组件名"></tr>
	// 这样我们设计的组件就会渲染出来了
</table>
```

### 1.18 watch

```js
// 1.第一种简单监听data中的值
data:{
    message:'你好'
}
watch:{
    message:function(newName,oldName){
        console.log('监听到message了')
        console.log('老旧'+oldName,'新的'+newName)
        // 当你修改message的时候 oldName就是你修改之前的 newName 就是改过来的
    }
}
// 2. immediate和handler
data:{
    message:'你好啊'
}
watch:{
    // 这种以一个对象的形式 里面可以配置
    message:{
        handler(newName,oldName){
            console.log('监听到了')
        },
        immediate:true
        // 如果为true 则第一次加载dom时就会触发这个handler 如果设置为false 则反之
    }
}
// 3.deep 深度监听
// 简单来说 如果在watch中设置deep为true的话 那么当你改data中对象中的属性的时候就会触发handler
data:{
    person:{
        name:'杜梦超'
    }
}

watch:{
    person:{
        handler(newName,oldName){
            console.log('监听深度')
        },
        deep:true
    }
}
// 这里要做一个优化 上面这么写 就会监听所有的 person中的属性 所以要针对性的监听的话 我们要改变一下
watch:{
    // 这里 以字符串的形式去监听
    'person.name':{
        handler(newName,oldName){
            console.log('监听深度')
        },
        deep:true
    }
}

```

### 1.19 this.$createElement 与this.$message

```js
this.$createElement(三个参数)
// 参数1 你要创建一个什么标签的 如div span
// 参数2 你希望给你创建的标签一个什么属性
// 参数3 你创建标签中的内容是什么

this.$message() // vue中封装的一个方法
// 这个方法 会将一个组件实例化并且可以往组件中传递参数然后放到页面上显示

// 举例
const h = this.$createElement;
this.$message({
    message: h(
        'div',
        { style: 'color: red; font-size: 14px' },
        body.map(x => h('div', null, x))
    ),
    type: 'warning'
});
// 利用 $createElement 创建一个标签
// 通过 $message将内容展示在页面上
```

### 1.20 v-for 和v-if 使用注意

```js
1.永远不要把v-if和v-for一起使用。如果你有一个列表并且只展现用户活跃的用户列表那么你直接弄一个计算属性将活跃的用户列表弄出来 然后直接v-for这个活跃列表就可以了
```

### 1.21 自定义组件

```html
<!-- 全局注册 在Vue.directive定义-->
<div id="app" class="demo">
    <!-- 全局注册 -->
    <input type="text" placeholder="我是全局自定义指令" v-focus>
</div>
<script>
    Vue.directive("focus", {
        inserted: function(el){
            el.focus();
        }
    })
    new Vue({
        el: "#app"
    })
</script>
<!-- 局部注册 在directives定义-->
<div id="app" class="demo">
    <input type="text" placeholder="我是局部自定义指令" v-focus2>
</div>
<script>
    new Vue({
        el: "#app",
        directives: {
            focus2: {
                inserted: function(el){
                    el.focus();
                }
            }
        }
    })
</script>
<!-- 对于binding参数 自定义的指令可以给参数 在bingding.value.参数名 去取-->
<div v-demo="{ color: 'white', text: 'hello!' }"></div>
<script>
    Vue.directive('demo', function (el, binding) {
    console.log(binding.value.color) // "white"
    console.log(binding.value.text)  // "hello!"
    })
</script>
```

- **el**: 指令所绑定的元素，可以用来直接操作 DOM，就是放置指令的那个元素。
- **binding**: 一个对象，里面包含了几个属性，这里不多展开说明，官方文档上都有很详细的描述。
- **vnode**：Vue 编译生成的虚拟节点。
- **oldVnode**：上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。

小案例

```html
<div id="app2" class="demo">
    <div v-for="item in imageList">
        <img src="../assets/image/bg.png" alt="默认图" v-image="item.url">
    </div>
</div>
<script>
    Vue.directive("image", {
        inserted: function(el, binding) {
            //为了真实体现效果，用了延时操作
            setTimeout(function(){
                el.setAttribute("src", binding.value);
            }, Math.random() * 1200)
        }
    })
    new Vue({
        el: "#app2",
        data: {
            imageList: [
                {
                    url: "http://consumer-img.huawei.com/content/dam/huawei-cbg-site/greate-china/cn/mkt/homepage/section4/home-s4-p10-plus.jpg"
                },
                {
                    url: "http://consumer-img.huawei.com/content/dam/huawei-cbg-site/greate-china/cn/mkt/homepage/section4/home-s4-watch2-pro-banner.jpg"
                },
                {
                    url: "http://consumer-img.huawei.com/content/dam/huawei-cbg-site/en/mkt/homepage/section4/home-s4-matebook-x.jpg"
                }
            ]
        }
    })
    // 实现一个当页面图片没有请求过来的时候先用一个默认的图片顶上 这里就可以用我们的自定义指令了
    // 这个自定义指令实现故意让设置好的图片慢一点放在上面 先用一个默认的图片放上面 然后指令中用一个settimeout时间到了之后给该标签设置一个src属性 这样就可以实现了
</script>
```



## 2.组件化

### 2.1 注册组件的基本步骤

1. 创建组件构造器
2. 注册组件
3. 使用组件

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>

<div id="app">
  <my-cpn></my-cpn>
</div>
<script src="../vue.min.js"></script>
<script>
  // Es6 Tab上面那个点也可以定义字符串，它可以换行

  // 1.创建组件构造器对象
  const cpnC = Vue.extend({
    template:`
    <div>
    <h1>我是标题</h1>
    <p1>我是内容</p1>
    <p1>哈哈哈</p1>
    </div>
    `
  })
  // 2.注册组件
  // Vue.component('使用的标签名','刚才注册构造器名字')
  Vue.component('my-cpn',cpnC)
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		}
	})
</script>
</body>
</html>
```

### 2.2 全局组件和局部组件

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn></cpn>
</div>
<script src="../vue.min.js"></script>
<script>
  // 创建构造器
  const cpnC = Vue.extend({
    template:`
    <div>
      <div>
        <h1>你好啊</h1>
      </div>
    </div>
    `
  })
  // 注册全局
  // Vue.component('cpn',cpnC) // 全局的，意味着可以在多个Vue实例中使用
  // 注册局部?在实例vue中使用看下面的 components
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
    components:{
	  // 这样注册就是局部的了 如果再写一个app02 然后挂载上 写这个cpn标签就不管用了
      // 使用的标签名:构造器名字
		  cpn:cpnC
    }
	})
</script>
</body>
</html>
```

### 2.3 父组件和子组件

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn2></cpn2>
</div>
<script src="../vue.min.js"></script>
<script>
  // 创建第一个组件
  const cpnC1 = Vue.extend({
    template:`
    <div><h1>我是cpnC1</h1></div>
    `
  })
  // 创建第二个组件（cpnC2是cpnC1的父亲 因为在cpnC2 里面注册了cpnC1）
  const cpnC2 = Vue.extend({
    template:`
    <div>
    <h1>我是cpnC2</h1>
    <cpn1></cpn1>
    </div>
    `,
    components:{ // 在构造组件化容器的时候可以在里面注册组件，注册之后就可以在这个模板里面使用你注册的组件了
      cpn1:cpnC1
    }
  })

	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
    components:{
		  cpn2:cpnC2
    }
	})
</script>
</body>
</html>
```

### 2.4组件语法糖

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn1></cpn1>
	<cpn2></cpn2>
</div>
<script src="../vue.min.js"></script>
<script>
	// 1.语法糖-全局
	Vue.component('cpn1',{
			template:`
			<div><h1>我是全局语法糖创建的</h1></div>
			`
		}
)
	// 2.语法糖-局部
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
		components:{
			cpn2:{
				template: `<div><h1>我是局部语法糖创建的</h1></div>`
			}
		}
	})
</script>
</body>
</html>
```

### 2.5 组件模板分离

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn></cpn>
</div>

<!--使用template标签可以做到分离-->
<template id="cpn">
  <div>我是分离出来的</div>
</template>
<script src="../vue.min.js"></script>
<script>
  Vue.component('cpn',{
    template:`#cpn`
    // 写分离的时候必须设置一个id 所以这里找到他需要使用#
  })
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		}
	})
</script>
</body>
</html>
```

### 2.6 组件如何使用胡子语法

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn></cpn>
</div>

<!-- 如果想访问必须在注册的 -->
<template id="cpn">
  <div>{{msg}}</div>
</template>
<script src="../vue.min.js"></script>
<script>
  Vue.component('cpn',{
    template:`#cpn`,
    data(){
      return {
        msg:'我是一个标题'
      }
    }
  })
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		}
	})
</script>
</body>
</html>
```

### 2.7 组件使用胡子语法时为什么data必须时函数

```javascript
	// 如果data还是原来那样写 那么就不具有隔离性了 就比如一个cpn组件 以后要复用 那么如果你使用它的时候，data原来是一个对象 那么它们都会指向同一个内存地址，这就导致了你一改变其他复用的也跟着变了
```

### 2.8  组件化-父子通信-porps

类似京东手机版的应用中 商品的瀑布流应该的数据不应该时每个商品都发一次请求吧？应该是全局发一次请求然后 再将数据发到这些子组件中进行使用的 这里就用到了 props 具体看代码的实现

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn :cmovies="movies" :cmessage="message"></cpn>
</div>
<template id="cpn">
	<div>
		<p>{{cmovies}}</p>
		<h1>{{cmessage}}</h1>
	</div>
</template>
<script src="../vue.min.js"></script>
<script>
	Vue.component('cpn',{
		template:`#cpn`,
		// props 中是你和父组件通信的桥梁 你自己定义一个名字 然后在使用这个标签的时候 v-bind:你定义的名字='你要绑定父亲的数据'
		// 1.第一种写法
		// props:['cmovies']

		// 2.第二种比较常用
		// 这种可以限制类型，还可以有默认值，还可以设置必须输入
		props:{
			cmovies:{
				type:Array,
				default:['aaaaa'],
				required:true
			},
			cmessage:{
				type:String,
				default(){
					return 'aaaaaaa'
				}
			}
		}
	})
	const app = new Vue({
		el:'#app',
		data:{
			message:'aaaa',
			movies:['钢铁侠','美国队长','肖申克']
		},
		component:{
			cpn
		}
	})
</script>
</body>
</html>
```

### 2.9 驼峰问题

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn :c-info="info" :c-my-message="message"></cpn>
</div>
<template id="cpn">
	<!-- vue中的模板必须用一个根元素包裹着 比如这个div	-->
	<div>
		{{cInfo}}
		{{cMyMessage}}
	</div>
</template>
<script src="../vue.min.js"></script>
<script>
	<!-- 如果出现驼峰的命名那么在真正使用标签的时候是不生效的 如何解决呢？	-->
	// cInfo 在真正使用的时候如果是这样命名的就改成 c-info 每个大写之前用一个-然后小写
	Vue.component('cpn',{
		template:`#cpn`,
		props:{
			cInfo:{
				type:Array,
				default() {
					return {}
				}
			},
			cMyMessage:{
				type:String,
				default:''
			}
		}
	})

	const app = new Vue({
		el:'#app',
		data:{
			message:'aaaaa',
			info:{
				name:'dmy',
				age:11,
				height:1.88
			}
		},
		component:{
			cpn
		}
	})
</script>
</body>
</html>
```

### 2.10 组件化-子传父

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<!-- 父组件 -->
<div id="app">
  <cpn @aclik="abclick"></cpn>
</div>
<!-- 子组件 -->
<template id="cpn">
  <div>
    <button v-for="item in tabbar" @click="itemclick(item)">{{item.name}}</button>
  </div>
</template>
<script src="../vue.min.js"></script>
<script>
  Vue.component('cpn',{
    template:`#cpn`,
    props:{
      tabbar:{
        type:Array,
        default:[
          {'id':1,'name':'家用电器'},
          {'id':2,'name':'游戏设备'},
          {'id':3,'name':'生活用品'}
        ]
      }
    },
    methods:{
      // 子向父传值
      // this.$emit('事件名',值)
      itemclick(item){
        this.$emit('aclik',item)
      }
    }
  })
	const app = new Vue({
		el:'#app',
		data:{
			message:'',
		},
    component:{
		  cpn
    },
    methods: {
		  abclick(item){
		    console.log(item,'我是父亲')
      }
    }
	})
</script>
</body>
</html>
```

### 2.11 组件化-案列

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn :number1="num1"
       :number2="num2"
       @exnum1 = "exnum1"
       @exnum2 = "exnum2"
  ></cpn>
</div>
<template id="cpn">
  <div>
    <h1>{{number1}}</h1>
    <h1>dnumber{{dnumber1}}</h1>
    <input type="text" :value="dnumber1" @input="changenum1">
    <h2>{{number2}}</h2>
    <h1>dnumber{{dnumber2}}</h1>
    <input type="text" :value="dnumber2" @input="changenum2">
  </div>
</template>
<script src="../vue.min.js"></script>
<script>
  // Vue.component('cpn',{
  //   template:`#cpn`,
  // })
	const app = new Vue({
		el:'#app',
		data:{
			num1:0,
      num2:1
		},
    methods:{
      exnum1(value){
        this.num1 = value
      },
      exnum2(value){
        this.num2 = value
      }
    },
    components:{
		  cpn:{
		    template: `#cpn`,
        props:{
		      number1:Number,
		      number2:Number
        },
        data(){
		      return{
		        dnumber1:this.number1,
		        dnumber2:this.number2,
          }
        },
        methods:{
          changenum1(event){
            this.dnumber1 = event.target.value
            this.$emit("exnum1",this.dnumber1)
          },
          changenum2(event){
            this.dnumber2 = event.target.value
            this.$emit("exnum2",this.dnumber2)
          }
        }
      }
    }
	})
</script>
</body>
</html>
```

### 2.12 $children-$refs

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
  <cpn></cpn>
  <cpn ref="aaa"></cpn>
  <cpn></cpn>
  <button @click="findechil">按钮</button>
</div>
<template id="cpn">
  <h1>我是子组件</h1>
</template>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
    methods: {
      findechil(){
        // 1.$children
        // 通过 父亲的 this.$children可以找到 父亲底下的所有子组件 也可以调用子组件的方法
        // 但是这个 $children用的比较少 开发时不会用这种方式去拿子组件
        // this.$children[0].showMessage()

        // 2.$refs 开发用的非常多
        // 前提是你在使用子子组件的时候需要加一个属性 也就是给一个key
        // 示例 <cpn ref="aaa"></cpn> 这样写完之后 就可以通过这个 aaa来找到了 并且能拿到里面的属性
        console.log(this.$refs.aaa.name)
      }
    },
    // 子组件
    components:{
		  cpn:{
		    template:`#cpn`,
        methods:{
		      showMessage(){
		        console.log('showMessage')
          }
        },
        data(){
		      return{
		        name:'哈哈哈'
          }
        }
      }
    }
	})
</script>
</body>
</html>
```

### 2.13 属性注意

```js
// 1.假设一个组件的内容时这样的
// myinput-item组件
<input type="date" class="form-control">
    
    
// 2.使用组件
<myinput-item
  data-date-picker="activated"
  class="date-picker-theme-dark"
></myinput-item> 

// 注意 如果你组件中已经定义了一些属性 那么你在使用组件的时候又重复定义了这些属性 那么 除了class和style之外的属性会被覆盖掉 class 和 style比较智能会添加到类中

// 如何禁用这种继承覆盖这种呢？

```



## 3 组件化进阶

### 3.1 slot插槽基本使用

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn><button>我是自定义1</button></cpn>
	<cpn><button>我是自定义2</button></cpn>
	<cpn></cpn>
	<cpn></cpn>
	<cpn></cpn>
</div>
<template id="cpn">
  <div>  <h1>我是子组件</h1>
  <!--
    1.slot 就是插槽 如果写了这个标签 在用子组件的时候 在子组件中写上 span 还是 button或者其他的 它会直接替换掉这个slot 如果一个子组件你写了多个span 它会一起替换掉
    2.slot 默认值 如果你slot中写了一个button 但是 你用的时候 子组件标签中什么都没写 那么会默认用这个button
  -->
    <slot><button>按钮</button></slot>
  </div>
</template>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
    components:{
		  cpn:{
		    template:`#cpn`
      }
    }
	})
</script>
</body>
</html>
```

### 3.2 slot 具名的使用

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
<!--
   1.使用 在模板中 给slot插槽定义一个name
   2.在使用组件的时候 如果你想替换其中的一个插槽 那么你替换的标签要加一个slot属性 并且属性的值 要对应你在模板中给的name值
-->
	<cpn><span slot="center">标题</span></cpn>
	<cpn><button slot="right">把右边变成按钮了</button></cpn>
</div>
<template id="cpn">
  <div>
    <slot name="left">左边</slot>
    <slot name="center">中间</slot>
    <slot name="right">右边</slot>
  </div>
</template>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
    components:{
		  cpn:{
		    template:`#cpn`,
      }
    }
	})
</script>
</body>
</html>
```

### 3.3 作用域插槽的使用

说白了就是 在插槽中使用的子组件的数据 怎么在使用组件的时候 自定义显示这个子组件的数据

```vue
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
<div id="app">
	<cpn></cpn>
  <!-- 如果我们想让这个子组件的数据以逗号搁开显示 不要以列表的方式显示怎么弄？ -->
  <!-- 写子组件模板的时候 插槽可以定义具名的name属性也可以定义 :data="你子组件中的一个数据" -->
  <!-- 用的时候需要写一个template 定义一个slot-scope属性去获取子组件中的值 slot-scope="名字" 名字.data就是刚才那个子组件传过来的值 -->
  <cpn>
    <template slot-scope="slot">
      <span v-for="item in slot.data">{{item}}</span>
    </template>
  </cpn>
  <cpn>
    <template slot-scope="slot">
    <!-- join 将列表中的元素以字符串显示 用什么连接起来 -->
      <span>{{slot.data.join(',')}}</span>
    </template>
  </cpn>
</div>
<template id="cpn">
    <div>
      <slot :data="languages">
      <ul>
        <li v-for="item in languages">{{item}}</li>
      </ul>
      </slot>
    </div>
</template>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
    components:{
		  cpn:{
		    template:`#cpn`,
        data(){
		      return{
		        languages:['python','java','php','c#','c++']
          }
        }
      }
    }
	})
</script>
</body>
</html>
```

### 3.4 v-slot

```vue
// 当定义了具名插槽 我们想用很多内容替换这一个插槽的时候就使用到了v-slot
<cpn>
    <template v-slot:你插槽定义的名字>
		你想用什么内容替换掉具名插槽呢？
    </template>	
</cpn>
```



## 4.模块化

### 4.1 ES6中的模块化

```javascript
// index 页面
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Title</title>
</head>
<body>
// 使用的时候 需要定义你导入的文件类型是 type
<script src="aaa.js" type="module"></script>
<script src="bbb.js" type="module"></script>
<script src="ccc.js" type="module"></script>
</body>
</html>
// aaa.js 文件
var flag = true
var name = 'dmy'


function sum(a,b) {
	console.log(a+b)
}

// 在模块化中 如果三个文件都使用了 type='module' 那么它们之间的变量函数是无法互通的 等于三个隔离的小房间
// 那么如果想使用 我们就用export 去导出

// 导出方式1
export {
	flag,sum
}

// 导出方式2
export var a = 1
export var b = 2


// bbb.js
// 通过 import { 你想使用的已经导出的变量或者函数} from '路径中的js文件'
import {flag,sum} from "./aaa.js";
// 这样就可以直接调用这个函数
sum(1,2)



// 导出类/函数

export function a(){
    console.log('我不好')
}

export Person(){
    run(){
        console.log('在奔跑')
    }
}

// 怎么使用呢
import {a,Person} from '....文件.js'

a()
// 实例化一个类
const p = Person()
// 调用类的方法
p.run()


// 导入全部
import * as app from '....文件.js'
// 使用
app.flag app.name
```

### 4.2 webpack 的使用和安装

#### 4.2.1 安装

首先去官网安装node 然后在终端

```
npm install webpack@3.6.0 -g
-g 就是安装到全局
```

#### 4.2.2 换源

```javascript
可用 get命令查看registry
1.
npm congfig get registry
原版结果为
2.
http://registry.npmjs.org
用set命令换成阿里的镜像就可以了
3.
npm config set registry https://registry.npm.taobao.org
再执行命令
4.
npm install
或者直接执行
5.
npm install --registry=https://registry.npm.taobao.org
```

### 4.3 使用webpack

#### 4.3.1 简单的使用

```javascript
// 第一步创建一个项目
// 目录结构
// 项目名
	// dist -> 这个是用来放打包后的最终js文件 用于给页面导入
	// src  -> 这个是写所有的脚本
		// main.js 这个就是接口文件 这里用来导入所有的模块
		// 剩下的js文件

// 终端命令
// 当你在main.js 中导入好了你所有的模块
// webpack ./src/main.js ./dist/bundle.js
// 这样操作之后 就会将接口文件 以浏览器认识的形式 全部放到 dist中的bundle文件中

// 这样操作之后 不管你有多少的js文件 只要导入 bundle整合好的js文件即可使用
```

#### 4.3.2 终端webpack 直接打包

```javascript
// 我们之前打包 要用 webpack 入口文件 出口文件 很麻烦 所以这里使用一种新的方式


// 1.创建 webpack.config.js 到项目中 名字不能换
// webpack.config.js
const path = require('path')

module.exports = {
	// 入口文件 这里可以写相对路径
	entry:'./src/main.js',
	output:{
		// 出口文件 这里必须要用绝对路径 所以我们要导入npm的一个依赖 path
		// 执行 npm init 和npm install 生成 package.json 和 pack-lock.json文件
		path:path.resolve(__dirname,'dist'),  // 拼接路径
		filename:'bundle.js' // 文件名
	}
}

// 之后在终端敲 webpack 就会自动将入口main.js打包到 bundle.js中了
```

#### 4.3.3 使用npm打包

之后的学习中 使用webpack 执行一些命令会比较复杂 可以使用npm 先配置命令

```javascript
// package.json文件
{
  "name": "meetwebpack",
  "version": "1.0.0",
  "description": "",
  "main": "webpack.config.js",
  // 找到这个scripts 这个就是npm可以执行的命令
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    // 看这里
    "build":'webpack'
    // 之后使用直接用 npm run build 就可以使用了
  },
  "author": "",
  "license": "ISC"
}

```

#### 4.3.4 注意

webpack 在终端 会找全局的 那么如果以后开发的时候 是接着别人的项目开发 人家用的是 3.6.0 你电脑里的全局是10.0.0 那么怎么办呢

```javascript
// 终端中安装局部
npm install--save-dev webpack@3.6.0
// --save-dev 是只有开发时才依赖
// 并且配置命令到 package.json中 用build来打包 他优先找项目中的本地webpack
```

#### 4.3.5 loader的使用

这里先注意一个问题 就是一定要配置 npm run build 命令

在package.json中的scripts脚本里面 配置一个 webpack命令

1. css 打包

```javascript
// 将src 分为 css js 目录结构 最外面写一个接口main.js

// index.css
body{
    background-color: red;
}

// main.js 如何导入呢
require('./css/index.css') // 直接导入即可 不用定义变量

// 这时候你再webpack是没有用的 需要loader依赖包
// 安装这两个依赖
npm install --save-dev style-loader
npm install --save-dev css-loader

// 在 webpack.config.js中也要加东西
module.exports = {
	entry:'./src/main.js',
	output:{
		path:path.resolve(__dirname,'dist'),  
		filename:'bundle.js' 
	},
    // 配置这个module
	module: {
		rules: [
			{
                  // 匹配css文件
				test: /\.css$/,
                  // 使用两个loader 顺序不能变 因为loader是从左往右 这里必须这样
				use: ['style-loader', 'css-loader'],
			},
		],
	},
}
```

#### 4.3.6 less样式 loader

```css
.less 文件
@fontSize:50px;
@fonColor:orange;
body{
  font-size: @fontSize;
  color: @fonColor;
}



# 在接口中 将less 文件导入 方式和css一样
# 其次从webpack 找到.less 的安装 及 rules的配置
# 如果报 getOption 则需要降低 --save 版本 百度就行
```

#### 4.3.7 图片的使用

```javascript
// 首先下载 url-loader 和 file-loader

// 看配置 webpack.config.js中
{
    test: /\.(png|jpg|gif|jpeg|PNG)$/,
        use: [
        {
            loader: 'url-loader',
                options: {
                    limit: 4000, // 这里设置80000 是因为我们用的测试图比较大 正常都是 8194
                        // 用来限制图片大小如果比这个值小 那么图片会以base64的编码格式放在页面上面
                        // 如果比这个值大 那么我们需要再安装一个 file-loader 来处理
                        // file-loader 处理
                        // name 的作用是为了 以后可能出现重复的图片名 就是比如home文件夹里面有一个 detail有一个 这俩都一样 那么页面生成的时候会冲突名字 所以这里可以设置name避免冲突
                        // hash:8 取八位哈希值 这里永远不会重复
                        name:'img/[name].[hash:8].[ext]'
            }
    },
    ],
},
    
.less 文件
@fontSize:50px;
@fonColor:orange;
body{
  font-size: @fontSize;
  color: @fonColor;
  background: url("../images/src=http___cdn.duitang.com_uploads_blog_201306_25_20130625150506_fiJ2r.jpeg&refer=http___cdn.duitang.jpg");
}
```

#### 4.3.8 ES6 转换成为ES5

因为有的浏览器还是不支持ES6 所以我们将之前打包好的ES6的 bundel,js 变成 ES5

```javascript
// 首先取webpack 安装babel-loader 不要加上后面的webpack 否则很麻烦
// 配置
{
    test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/,
            use: {
                loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env']
                    }
            }
}
```

#### 4.3.9 Vue的配置

```javascript
npm install vue --save
// 注意这里不加 -dev 因为这里并不是开发时依赖在以后写项目的时候也要用到

// main.js
import Vue from "vue";
const app = new Vue({
	el:'#app',
	data:{
		message:'Hello Vue'
	}
})
// 这里这么写之后页面渲染的时候还是会有问题 说你正在使用run-timeonly 这个是不支持编译template
// 解决办法： 配置 在webpack.config.js 配置一下就行 具体什么位置看示例
resolve:{
    alias:{
        'vue$':'vue/dist/vue.esm.js'
    }
}
```

#### 4.3.10 el和tempalte

在之后的开发中 其实只是写一个index.html 并且里面只挂载一个app里面也没有任何胡子语法 因为我们需要在js中注册vue的app中写template

```javascript
const app = new Vue({
	el:'#app',
	template:`
		<div>{{message}}</div>
	`,
	data:{
		message:'Hello Vue'
	}
})
// 这里面的template 会自动替换掉el挂载的app
```

#### 4.3.11 Vue终极

```javascript
// 我们不可能把模板就直接放在 template中直接编写会非常麻烦 所以这里采用一种新的方式
// 首先安装 vue-loader 和 vue-template-compiler
// 生产时依赖 --save-dev

// 注意：安装好的配置文件中的vue-loader需要更改一下版本 改成13.0.0这个版本 重新 npm install 一下


// 使用
// 我们可以在src中创建vue文件 并且创建后缀时.vue的文件 举个例子
// 创建好之后 它会自动分出来 模板 脚本 样式
App.vue
<template>
  <div>
  <div class="title">{{message}}</div>
  <Cpn/>
  </div>
</template>
<script>
// 又引入了一个组件
import Cpn from "./Cpn.vue";
export default {
  name: "App",
  data(){
    return {
      message:'你好啊 Vue'
    }
  },
  components:{
    Cpn
  }
}
</script>

<style scoped>
.title{
  color: rebeccapurple;
}
</style>


// main.js 使用
// 导入vue
import Vue from "vue";
import App from './vue/App.vue'
const app = new Vue({
	el:'#app',
	template:`<App/>`,
	components:{
		App
	}
})
```

#### 4.3.12 html-webpack-plugin

```javascript
// 首先安装
npm install html-webpack-plugin@3.2.0 --save-dev
// 这个插件的作用是 之后项目上线的时候其实只将dist文件上传 所以index.html也需要在dist中 我们之前是在 跟dist同级的目录中 利用这个插件 可以自动生成

// 第二步 配置
// plugins 是配置中的专门写接口的部分
plugins:[
    new HtmlWebpackPlugin({
        // 找到模板我们之前写的index.html
        template:'index.html'
    })
]
// 将原来写的index.html 放入其中的模板中

//执行 npm run build 这时候 dist会自动生成一个index.html
```

#### 4.3.13 丑化JS代码(节省空间)

```javascript
// 为了节省空间 我们的bundle.js 需要丑化
// 第一步安装
npm install uglifyjs-webpack-plugi
n@1.1.1 --save-dev
// 引入+使用
const uglifywebpackPlugin = require('uglifyjs-webpack-plugin')
new uglifywebpackPlugin() // 放在plugin中
```

#### 4.3.14 webpack-dev-server

这个插件的目的是为了在本地搭建一个服务器 跟python的run server 差不多

```javascript
// 第一步安装
npm install webpack-dev-server@2.9.3 --save-dev
// 配置
devServer:{
    contentBase:'./dist',
    inline:true
}
// 配置2 需要指定一个命令
// package.json 配置命令那里加一个
"dev": "webpack-dev-server --open chrome"
// --open运行时自动打开浏览器 chorome 默认谷歌浏览器
// 执行
npm run dev
```

#### 4.3.15 webpack 配置分离

```javascript
// 首先安装
npm install webpack-merge --save-dev
// 创建一个 build文件里面创建三个文件
// 一个是基础的配置就是不管是生产还是上线都需要用到的
// 一个是生产时的
// 一个时上线用的

// 基础配置就将所有的 生产和上线的配置信息都删掉

// 生产时的文件
const webpackMerge = require('webpack-merge')
const baseConfig = require('base.config')
// 将基础文件和当前生产时候需要的配置 柔和在一起
module.exports = webpackMerge.merge(baseConfig,{
	devServer:{
		contentBase:'./dist',
		inline:true
	}
})
// 上线
const uglifywebpackPlugin = require('uglifyjs-webpack-plugin')
const webpackMerge = require('webpack-merge')
const baseConfig = require('./base.config')
module.exports = webpackMerge.merge(baseConfig,{
	plugins:[
		new uglifywebpackPlugin()
	]
})


// 注意 还有一些配置需要更改首先如果你直接执行npm run build 那么它不会打包在原来的dist中而是找到了build 文件 所以需要更改
package.json 中
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
   	// 上线时 需要执行 build 所以配置文件是上线的
    "build": "webpack --config ./build/prod.config.js",
    // 生产时 只需要搭建本地服务器测试即可 所以这里时 生产的配置
    "dev": "webpack-dev-server --open chrome --config ./build/dev.config.js"
},
```

## 5.脚手架

### 5.1基本使用

#### 安装

```javascript
npm install -g @vue/cli
// 如果想即用脚手架2 又想用脚手架3
npm install @vue/cli-init -g
```

#### 创建一个项目

先基于脚手架2来创建项目

```vue
vue init webpack 项目名称
```

基于脚手架3

```
vue create 项目名称
```



#### 关掉eslint

怎么关掉eslint呢？ 就是这个标准

找到config中的index.js 里面有一个UseEslint 把它置为false

#### runtime-only 和runtime-compiler

```js
// 开发时大多用runtime-only 因为太省去了编译 并且代码量可少 性能更高
// 所有的template 都会被装的 vue-template-complier 解析 所有的template都会变成render函数这是对于runtime-only来说
```

#### 关于脚手架3得0配置

因为脚手架3 将配置文件都放在了包中没有放在外面所以如果你对它默认得配置不满意想要修改得话 在项目目录中创建一个vue.config.js 并且在里面这么写

```javascript
module.exports = {
	
} // 这里面写得内容会和默认得自动融合在一起

```

### 5.2 箭头函数得使用

```javascript
// 1.对于只有一个参数的情况
const a = a => {
    console.log('演示只有一个参数')
}

// 2.只有一行返回 它会自动返回
const sum = (num1,num2) => num1+num2

```

#### 关于this得指向

```javascript
const a = {
    aaa(){
        setTimeout(function (){
            console.log(this) // window
            setTimeout(()=>{
                console.log(this) // window
            })
        });
        setTimeout(function(){
            console.log(this) // window
        });
        setTimeout(()=>{
            console.log(this) // obj
        })
    }
}
a.aaa()
// 总结 凡是 function(){} 这种没有命名得这种形式 它们得this全是window 因为在调用call方法得时候内部是传入了window参数
// 箭头函数得this会往上找 上一层得this是什么 它就是什么
```

### 5.3  navigator

```js
// 在国际化的时候我们可以通过 navigator.language 来获得用户的首先语言
```



## 6.Vue-router

### 6.1 前端路由的映射

建立 url与组件之间的映射关系

这种机制不是前后端分离而是只有一套html+css+js 然后配置一个前端得路由 在请求得时候只请求一次 就将所有得一套都请求下来 然后根据url映射得不同从那一套中抽离出数据展示在页面上 页面也是只有一个的 只不过根据前端路由的映射去那一套里面拿

```javascript
// 1.通过location.hash
通过 location.hash = ‘aaa’
这样改页面不会刷新
// 2.通过history.pushState 和 history.back
history.pushState({},'','home')
// 这就相当于一个栈 往里面压入了一个home 然后页面就会后面跟着一个/home 如果你再调用这个方法然后压入一个detail 那么后缀就变成了/detail
history.back()// 将你栈顶的 弄出去然后就会显示下一个了

// 3.通过replaceState()
history.replaceState({},'','home')
// 这是通过一种替换的方式就是没有历史记录 直接替换
```

### 6.2 使用

```js
// 1.导入
import Router from 'vue-router'
// 2.以后所有的插件都需要.use使用
Vue.use(Router)
// 3.使用并且导出准备给Vue实例使用
// 这里我给抽离出去来了 然后下面用了一个es6的增强语法 给它导出出去
const routes = [
  {
  path: '/',
  name: 'HelloWorld',
  component: HelloWorld
  }
]
export default new Router({
  routes
})
```

### 6.3 页面进行切换

```js
// <router-view/>标签 是用来显示你其他组件的内容的

// 对于routeru-link标签的使用
// 1.to
// <router-link to='/home'>回家</router-link>
// 点击时会跳转到你写好的vue组件中并将内容显示在<router-view/> 这个标签这里

// 2.tag
// router-link 默认会渲染成a标签 怎么改？
<router-link to='/home' tag='button'>
    
// 3.replace
<router-link to='/home' tag='button' replace>
// 这个replace 是用于使用history.replaceState
// 作用就是不允许通过浏览器的后退按钮进行跳转只能点击router-link标签
    
// 4.active
// 当一个router-link点击的时候 那么它就会默认给标签添加一个router-link-active的类属性 以后可以根据这个属性给被选中的标签改样式
    
// 5.如何改这个class 名字呢
export default new Router({
  routes,
  mode:'history',
  linkActiveClass:'active'
})
```

### 6.4 重定向默认页面

```js
const routes = [
  {
    // 默认路径
    path: '/',
    // 重定向到哪个页面
    redirect:'/home'
  },
  {
    path: '/home',
    name: 'Home',
    component: Home
  }
]
```

### 6.5 如何从hash变成history

```js
// http://localhost:8080/#/home 从这种变成下面这种
// http://localhost:8080/home
export default new Router({
  routes,
  // 以前有#号是hash 这里改下模式
  mode:'history'
})
```

### 6.6 如何不通过router-link来跳转

```javascript
<button @click="helloClick">哈喽</button>
export default {
  name: 'App',
  methods:{
    helloClick(){
      this.$router.push('/hello')
    }
  }
}
// 每一个组件都有一个 this.$router 可以实现跳转
```

### 6.7动态路由

#### 6.7.1 传值

```js
// 1. 配置一个路由
{
    // user/:userId 允许传值
    path: '/user/:userId',
        component: User,
}
// 2.在使用 router-link 使用v-bind语法糖绑定值
<router-link :to="'/user/'+userId">回家</router-link>
// 组件中需要有一个data定义这个userID
data(){
    return{
        userID:'dmy'
    }
}
// 完成
```

#### 6.7.2 将传的值页面中使用

```js
// 这里用计算属性来演示
computed:{
    userId(){
        return this.$route.params.userId
    }
},
// this.$route.params.（你分配路由时候的参数）
```

#### 6.7.3 $route的一些属性

```js
$route.path // 对应当前路由的绝对路径
$route.params // 获取的一个对象，对象中是key-value的形式，如果没有就是空对象 /user/:id
$route.query // 获取一个对象，表示url的查询参数，比如/user/?id=1，$route.query.id为1
$route.name  // 当前路由的名称，建议写路由的时候给每一个都来一个name,以后的开发中更清晰
$route.fullPath // 当前路由的URL包含查询参数
$route.matched // 类型是一个数组，它包含当前路由从上到下的包含关系
```



### 6.8 路由懒加载

```js
// 当打包之后 会生成三个js 一个全部逻辑的代码 一个依赖包的代码 一个底层支撑的代码
// 可想 如果以后的逻辑代码有特别特别的多 那么用户加载的时候一下子全加载下来是特别影响性能的 那么我们要实现一种懒加载 比如先访问首页那么就先加载首页的 像我的 购物车这种的js文件先不加载什么时候用什么时候加载


// 实现
// 懒加载 利用箭头函数的形式把组件导入 并且在下面分配的时候使用
const Home = ()=>import('../components/Home')
const HelloWorld = ()=>import('../components/HelloWorld')
const User = ()=>import('../components/User')

const routes = [
  {
    path: '/hello',
    component: HelloWorld
  },
  {
    // 默认路径
    path: '/',
    // 重定向到哪个页面
    redirect:'/home'
  },
  {
    path: '/home',
    name: 'Home',
    component: Home
  },
  {
    // /:userId 允许传值
    path: '/user/:userId',
    component: User,
  }
]
// 此时你再进行npm run build 每个组件都会生成对应的js组件
```

### 6.9 路由的嵌套

```js
// 分配路由的时候有一个 children
  {
    path: '/home',
    name: 'Home',
    component: Home,
    children:[
      {
        // 设置个默认值 用户进入首页新闻自动显示出来
        path:'',
        redirect:'news'
      },
      {
        path: 'news',
        component:HomeNews
      },
      {
        path: 'message',
        component:HomeMessage
      }
    ]
  },
// 在home中嵌套的子路由那么 你需要在Home的组件中使用router-link
// 并且你所显示的内容 也要在这个home中用 router-view 来显示嵌套路由的内容
<template>
<div>
  <h1>我是家</h1>
  <h2>我是Vue家</h2>
  <router-link to="/home/news">新闻</router-link>
  <router-link to="/home/message">消息</router-link>
  <router-view/>
</div>
</template>
```

### 6.10 编程式导航的写法(利用js跳)

```js
/*
	之前我们跳转页面的时候是配置router-link标签来实现的，我们也可以利用js代码进行跳转
*/

// 1.$router.push
// <router-link to='/user'></router-link>
this.$router.push('/user') // push与上面的to跳转效果一样的
this.$router.push({path:'user'}) // 传入一个对象，对象中有path属性也可以实现
this.$router.push({name:'xiaowang',params:{userId:1}})// 通过命名路由跳转
this.$router.push({path:'user',query:{planId:1}}) //带查询参数进行跳转

/*
	注意
		path和params是不能同时生效的!,否则params会被忽略掉.所以使用对象写法进行params传参时,要么就是path加冒号:,要么就是像上例中的'命名路由'.通过name和params进行传参.然而query却并不受影响,有没有path都可以进行传参.
*/
// 2.$router.replace
/*
	用法与push相似，但是效果不一样，比如你用push你从a页面到b页面你会压入b页面入栈，回退的时候会找到a页面而replace不一样，他是将a页面替换为b页面时无法进行回退的，什么时候用呢，就是比如有验证的页面你不想让用户回退回去可以使用这种
*/


// 3.简单使用
<router-link :to="{path:'/profile',query:{name:'dmy',age:15,height:'1米7'}}">档案</router-link>

// 如何将query的值展示呢？ 看跳转过去的页面
<div>
  <h1>我是一个Profile</h1>
  <h2>{{$route.query.name}}</h2>
  <h2>{{$route.query.age}}</h2>
  <h2>{{$route.query.height}}</h2>
</div>

// 如何利用监听按钮事件来跳转并且携带这个query呢？
<button @click="userprofile">档案</button>


userprofile(){
    this.$router.push({
        path:'/profile',
        query:{
            name:'lbj',
            age:37,
            height:'两米了',
        }
    })
}
// 拿数据还是和上面一样的 
```

### 6.11 守卫

#### 1.全局守卫

```js
// 需求：每当跳转一个页面时 浏览器显示的title为当前页面定义好的title
// 这里涉及到router.beforeEach
router.beforeEach((to,from,next)=>{ // 这个是在跳转之前执行的
  // from:从哪个页面来的
  // to:到哪个页面去
  // 跳转时触发 将title命名
  document.title = to.matched[0].meta.title
  // 这个to 如果你重写了这个beforeEach 那么必须触发这个next() 否则无法跳转
  next()
})
```

#### 2.路由独享守卫

```js
// beforeEnter 路由只独享这一个钩子 在routes中配置
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // 使用方法和上面的beforeEach一毛一样
      }
    }
  ]
})
```

#### 3.组件内的守卫

```js
/*
3,组件内的守卫: 注意:这类路由钩子是写在组件内部的,
beforeRouteEnter 进入路由前,此时实例还没创建,无法获取到zhis
beforeRouteUpdate (2.2) 路由复用同一个组件时
beforeRouteLeave 离开当前路由,此时可以用来保存数据,或数据初始化,或关闭定时器等等
*/
const Foo = {
  template: `...`,
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    // 不！能！获取组件实例 `this`
    // 因为当守卫执行前，组件实例还没被创建
  },
  beforeRouteUpdate (to, from, next) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
  },
  beforeRouteLeave (to, from, next) {
    // 导航离开该组件的对应路由时调用
    // 可以访问组件实例 `this`
  }
}
```



### 6.12 keep-alive

所有路径匹配到的视图都会被缓存

举例：进入一个页面默认展示的是消息列表，你点击了一个新闻列表然后你跳转到了另一个页面你希望再回来的时候还显示新闻列表

```js
// 1. 只有在使用keep-alive 缓存的情况下才可以使用 actived 和 deactived
<keep-alive>
	<router-view/>    
</keep-alive>
// 2.具体实现就是在活跃的钩子中记录你当前的url 非活跃的时候将url保存下来
data(){
    return{
        path:'/home/news'
    }
}
actived(){
    this.$router.push(this.path)
    // 刚进来时 默认进入新闻页面
}
deactived(){
    // 在离开页面时将你当前的url保存 就是给data中的path赋值
    // 比如你点了消息页面 那么就将消息页面的url保存 在下一次进入该页面的时候直接出发actived函数
    this.path = this.$route.path
}
```

### 6.13 keep-alive的属性

我们希望有一些路由页面可以创建和销毁而不是活跃与不活跃

```js
// 这是档案的js代码 这个name可以用于 keep-alive 排除
<script>
export default {
  name: "Profile"
}
</script>

<keep-alive exclude="Profile"> // 如果想多个排除 直接 Profile,User 
	<router-view/>    
</keep-alive>
```

### 6.14 render函数

```js
// 需求：创建一个锚点子模块在点击的时候根据传入的id生成一个锚点
// 传统写法 子模块中利用v-if 判断所有传入的level 会非常冗余 并且每个level的锚点都需要写一个插槽也很冗余

// render函数里面可以写模板
Vue.component('anchored-heading', {
  render: function (createElement) {
    return createElement(
      'h' + this.level,   // 标签名称
      this.$slots.default // 子节点数组
    )
  },
  props: {
    level: {
      type: Number,
      required: true
    }
  }
})
```

### 6.15 别名 alias

```js
// 一个路由的名字可能有很多个，都指向这个一个路由
const router = new VueRouter({
//这时,路径'/fxxksky'和'/two-dogs' 都会跳转到A
  routes: [
    { path: '/fxxksky', component: A, alias: '/two-dogs' }
	//当有多个别名时,alias也可以写成数组形式.  alias: ['/two-dogs', 'three-dogs','four-dogs','five-dogs'] 
  ]
})
```

#### 6.16 meta元数据

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      children: [
        {
          path: 'bar',
          component: Bar,
          // a meta field
          meta: { requiresAuth: true }
        }
      ]
    }
  ]
})
// 简单来说元数据就是路由里的meta对象中的数据
// 用途？下面看一个关于用户的登录的例子
router.beforeEach((to, from, next) => {
  if (to.matched.some(record => record.meta.requiresAuth)) {
    // 对matched不了解的建议看官方api文档,或我7.1节的说明
    // 数组some方法,如果meta.requiresAuth为ture,则返回true.此时,说明进入该路由前需要判断用户是否已经登录 
    if (!auth.loggedIn()) {   //如果没登录,则跳转到登录页
      next({
        path: '/login',
        query: { redirect: to.fullPath }  //官方例子的这个小细节很好,通过query将要跳转的路由路径保存下来,待完成登录后,就可以直接获取该路径,直接跳转到登录前要去的路由
      })
    } else {
      next()
    }
  } else {
    next() // 确保一定要调用 next()
  }
})
```



## 7.小案例-tabbar

### 7.1 关于css样式的引用

```php+HTML
// 1.有一些初始化的样式 我们不能写在入口的main.js去引入 也不能直接堆到style中 所有我们需要使用@import

<style>
    @import "./css文件的路径";
</style>
```

### 7.2 box-shadow

```css
#box{
	box-shadow:10px 10px 1px red
}
1.盒子阴影 前两个参数是只x轴和y轴的偏移 如果这么设置就是往下和往右 如果是负值就是往左和往上 第三个参数是阴影的模糊半径 第四个则是颜色
```

### 7.3 indexOf使用

这里为了实现tabbar点击哪个哪个活跃 用到了这个

```js
// 此方法对大小写是敏感的
// 如果检索的字符串没有出现 则返回-1
computed:{
    isActive() {
        // 等于-1就代表没找到 不等于-1就是找到了
        // 如果当前页面的路径中 和其中一个tabbar-item 中的link是相符合的 那么这里就返回true 其他 的tabbar-item中的isActive就是false
        return this.$route.path.indexOf(this.link) !== -1
    }
},
```

## 8 Vuex

### 8.1 安装与导入

```js
// 1.安装
npm install vuex


// 2.导入
// 3.在项目中创建一个store文件夹里面创建一个index.js
// index.js
import Vue from 'Vue'
import Vuex from 'Vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
    ...
})
    
export default store
    
    
// 项目的main.js
import Vue from 'Vue'
import store from './store'
new Vue({
  el: '#app',
  store,
  router,
  render: h => h(App)
})
// 这样将store放进去 Vue内部会 Vue.prototype.$store = storev 
```

### 8.2  使用 

```html
<script>
// action 的作用就是如果有异步操作 要弄一个这个action
// mutations 在对状态进行修改的时候 应该在这里修改 因为这样才能监听到是谁修改了或者说是操作了这个数据 在改bug的时候比较方便


// 使用
// store 中
const store = new Vuex.Store({
    state:{
        counter:1000
    },
    // 如果在组件中想要改变数据 应该在mutations中定义改变数据的方法
    // 在使用的时候 不是直接调用$store.increament 而是 this.$store.commit('方法名')
    mutations:{
        increament(state){
            state.counter++
        },
        subaction(state){
            state.counter--
        },
        addcounter(state,count){
            state.counter += count
        }
    }
})
</script>


// 组件中使用
<body>
<div id="app">
	{{count}}
	<button @click="addlition">+</button>
	<button @click="sublition">-</button>
    <button @click="addcounter(5)">加5</button>
    <button @click="addcounter(10)">加10</button>
</div>
<script src="../vue.min.js"></script>
<script>
	const app = new Vue({
		el:'#app',
		data:{
			message:''
		},
		computed:{
			count(){
				return this.$store.state.count
			}
		},
		methods:{
			addlition(){
				this.$store.commit('increament')
			},
			sublition(){
				this.$store.commit('subaction')
			}，
            addcounter(count){
        		this.$store.commit('addcounter',count)
    		}
		}
	})
</script>
</body>
```

### 8.3 getters的使用

```html
<script>
import Vuex from 'Vuex'
import Vue from 'Vue'

const store = new Vuex.Store({
    state:{
        couter:10
        messages:[
            {'id':1,'age':10},
            {'id':2,'age':15},
            {'id':3,'age':20},
        ]
    }
    getters:{
    	// 1.获取counter的平方 这个state在使用的时候不需要传 内部已经传好了
        powercounter(state){
    		return state.counter * state.counter
		}
    	// 2.获取年龄大于age的 写一个通用的函数组件在用的时候可以传递参数
    	getagelist(state){
       		// 返回一个函数
            return age => state.message.fillter(s => s.age> age)
        }
	}
})   
</script>

<body>
    使用
    <div id='app'>
        获取全局counter的平法
        {{counterpower}}
        获取年龄大于age的
        // 因为我们上面getagelist返回一个函数那么这里不加括号就是那个函数然后加括号就是执行我们返回的函数
        {{$store.getters.getagelist(12)}}
    </div>
</body>

<script>
	const app = new Vue(
        el:"#app",
        computed:{
        	counterpower(){
        		// 调用getters时不用加括号
        		return this.$store.getters.powercounter
    		}
        }
    )
</script>
```

### 8.4mutations  payload的使用

```php+HTML
<script>
    //mutations.js
    export default = {
        modifynum(state,payload){ // payload 可以在组件中使用的时候传入
            state.userinfo.age += payload.num
        }
    }
    // 组件中
    methods:{
        modifyage(){ // commit 第二个参数是一个对象 对应的就是payload
            this.$store.commit('modifynum',{
                num:1
            })
        }
    }
</script>


<script>
	// 在执行commit的时候是可以传递参数的 但是还有另外一种传递方式 payload
    // 1.组件中
    methods:{
        addcount(){
            return this.$store.commit({
                type:'addcounter' // 你在mutations 中定义的方法
                count // 你想传递的参数
            })
        }
    }
    
    // 2.index.js中
    const store = new Vuex.Store({
        state:{
            count:1
        }
        mutations:{
        	addcounter(state,payload){
        		// payload 就是你commit传入的对象
        		state.count += payload
    		}
    	}
    })
</script>
```

### 8.5 响应式系统state

要做到响应式前提是你state中都定义好的数据 你往里面添加数据是无法做到响应式的

解决办法

```vue
Vue.set('对象','key名','值') // 这样可以做到响应式
Vue.delete('对象','key名')
```

### 8.5 对于mutations中的命名

不容易写错，字符串容易写错，而且字符串写错以后不会报错位置，而用常量替代，如果写错，eslint可以提示错误位置

当使用action派发mutation时，在action中使用同样的常量，避免手滑写错方法

1.弄一个统一的mutations-type.js文件

```js
export const Increament = 'Increament'
// 以后都以这种形式将Mutations的名字进行导出 这样不管你咋改这里的名字都不会影响
```

2.store使用

```js
import {Increament} from './mutations-type'
mutations:{
    [Increament](state){
        ....
    }
}
```

3.模板中使用

```js
import {Increament} from './mutations-type'

methods:{
	countpower(){
		return this.$store.commit(Increament)
	}
}
```

### 8.6 action 异步处理

```js
/*
    action可以提交mutation,然后mutation去更改state
    action不要直接去操作state，而是去操作mutation
    action包含异步操作，类似于axios请求，可以都放在action中写
    action中的方法默认的就是异步，并且返回promise
*/

// 简单使用
import {
    ADD_AGE,
    CHANGE_NAME,
    ADD_FRIEND,
    SET_USER_INFO,
    SET_TOKEN
} from "./mutation_type.js"

export default{
   //定义一个异步获取用户信息的action
    
    async getUserInfo(context){
       //context可以理解为它是整个Store的对象.类似于this.$store，里面包含了state，getter，mutations，actions
       const res = await axios.get('/接口url')
       
       //这个时候就用到了 mutation_type.js
       context.commit( SET_USER_INFO,{userInfo:res.userData}
       )
    },
    
    //定义一个异步获取用户token的action
    async getToken(context){
         const res = await axios.get('/接口url')
         context.commit(
             SET_TOKEN,
             {token:res.token}
       )
    }
    
}
// 解构
async getToken({commit,state}){
    const res = await axios.get('/接口url')
    commit(SET_TOKEN,{token:res.token})
}



// 需求 我们希望做一个简单的异步 一秒之后修改count 并且改完有通知 用到了Promise


mutations:{
    ltationcount(state){
        state.count += 1
    }
}
// store中
// context 是上下文可以理解为就是store payload就是组件使用这个的时候传入的值
actions:{
    editcount(context,payload){
        return new Promise((resolve,reject)=>{
            setTimeount(()=>{
                context.commit('ltationcount')
                console.log(payload)  // 你好啊
                resolve('111')
            },1000)
        })
    }
}


// 组件中 注意看then
methods:{
    editcount(){
        this.$store.dispatch('editcount',{
            message:'你好啊'
        }).then(res=>{
            console.log(res) // 111
            console.log('处理完成了')
        })
    }
}

// action中返回一个Promise 那么你调用this.$store.dispatch()就会得到那个Promise 你在Promise又已经做完了异步的操作了 然后等于做了一个中转 在这边返回Promise直接调用then可以完成接到res参数
```

### 8.7 mouduls

```js
const moduleA = {
    state:{
        name:'dmy'
    },
    mutations:{
        editName(state,payload){
        	state.name = payload
        }
    },
    getters:{
        getnames(state){
            return state.name + '111'
        },
        getnames1(state,getters){
            return getters.getnames + '222'
        }
    },
    actions:{
        increament(context){
            console.log(context) // 因为这里是module写的所以这里打印可以看到 rootgetters rootstate 可以找到根store 但是在底下的actions中打印context 就没有根了
            setTimeout(()=>{
                 context.commit('editName','l')
            },1000)
        }
    },
}

const store = Vuex.Store({
    modules:{
        a:mouduleA
    }
})


// 组件中使用
{{getname}}
{{editname('lisi')}}
methods:{
    getname(){
        return this.$store.a.name // 这里不用a.state.name 直接name就可以
    },
    editname(name){
        return this.$store.commit('editName',name) // 这个虽然是在模块a中的一个mutation但是使用的时候不用.a 直接commit这个名字即可 dispatch同理
    },
    asyncname(){
        this.$store.dispatch('increament')
    }
}
```

### 8.8 mapState辅助函数

```js
// 获取state时 我们可以写一个计算属性 但是如果有特别多的状态你需要写特别多的计算属性
computed:{
    userName(){
        return this.$store.state.userInfo
    }
    ... 好几十个呢？
}
// 所以 vuex 给了一个辅助函数 mapState
computed: mapState(['likes','friends','token','userInfo'])
// 这样就等价于自动映射除了很多计算属性

// 但是 这样会有一个问题 如果我们想自定义别的计算属性呢 这时候要用的...
computed: {   
  value(){
   return this.val++
  },
  ...mapState(['likes','friends','token','userInfo'])
}


// 关于别名
computed: {   
  value(){
   return this.val++
  },
  ...mapState({
      myLikes:"likes",
      myFriends:"friends",
      theUserInfo:"userInfo"
  })
}
// 使用  {{ theUserInfo.username }} 给state中的userInfo起一个别名叫theUserInfo
```

### 8.9 mapGetters辅助函数

```js
/*
	getters相当于vue中的计算属性，能拿到state里面最新的值

	而且getters允许传参，第一个参数就是state

	这样，通过getters进一步处理，得到我们想要的值，
*/

// 先看 getters.js 中 里面两个可以获取state中的数据
export default{
    realName:(state)=>{
      return state.userInfo.userName+''
    },
    myMoney:(state)=>{
      return (state.money/7).toFixed(2)
    }
}


// mapGetters 使用
computed(){
    value(){
        return '值'
    },
    ...mapGetters([realName,myMoney]) // 使用方法和 state差不多
}

// 别名
computed: {  
 valued(){
   return this.value++
 },
 ...mapGetters({
     myRealName:"realName",
     myFormatMoney:"myMoney"
 })
}
```

### 8.10 mapMutations  辅助函数

```js
// mutations.js
export default = {
    modifynum(state,payload){ // payload 可以在组件中使用的时候传入
        state.userinfo.age += payload.num
    }
}

// 实例中使用
methods:{
 ...mapMutations(['modifynum'])
}
// 实例中使用 传递payload
{{ modifynum({num:1}) }}



// 别名也ok
methods:{
 ...mapMutations({
     modifynumber:modifynum
 })
}


// 我们为啥要绕一圈修改state中的值呢 为啥不这样
this.$store.state.userInfo.age += 5 // 为啥不这样？
/*
	Vue.js在mutations中做了类似埋点操作，如果从mutations中操作的话， 能被检测到，可以更方便用调试工具调试，调试工具可以检测到实时变化，而直接改变state中的属性，则无法实时监测
*/
```

### 8.11 mapActions辅助函数

```js
methods:{
    ...mapActions([requestUser,requestProfile])
}
// 别名
methods:{
    ...mapActions({
        user:requestUser,
        profile:requestProfile
    })
}

// 补充 action中可以调用别的action

export default {
    async requestUser(context){
        const res = await axios.get('/url地址')
        context.dispatch('requestProfile')
    }
    async requestProfile(context){
        const pro = await axios.get('/url地址2')
        context.commit(SET_PROFILE,pro)
    }
}
```

### 8.12 简单总结

1. 依赖state得到新的数据，用this.$store.getters.值
2. 直接获取state的数据，用this.$store.state.值
3. 同步修改state的属性值，就用this.$store.commit('mutation值')
4. 异步修改state的属性值，就用this.$store.dispatch('action值')
5. mapState、mapMutations、mapGetters、mapActions等辅助函数，便于我们处理多个方法和属性
