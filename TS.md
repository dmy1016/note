# TS

```typescript
// 安装
npm install -g typescript
// 编译 ts文件
tsc 文件名.ts
```



## 1.基础数据类型

### 1.1 Boolean

```typescript
let isDone:boolean = true
console.log(isDone) // true
```

### 1.2 Number

```typescript
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
let bigLiteral: bigint = 100n;
```

### 1.3 String

```typescript
let name : string = 'dmy'
let sentence : string = `hello ${name}`
```

### 1.4 Array

```typescript
let arry1 : number[] = [1,2,3]
// 规定这个数组中只能放number的类型的元素

let arry2 : Array<number> = [3,4,5]
// 使用数组泛型也可以定义
```

### 1.5 Tuple

```typescript
let x:[string,number]
x = ['aaa',1] // 这是OK的
x = [1,'aaa'] // Initialize it incorrectly

// 当访问一个已知的元素会得到正确的类型
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'

// 如果越界访问
console.log(x[5].toString())// Error, Property '5' does not exist on type '[string, number]'.
x[3] = "world"; // Error, Property '3' does not exist on type '[string, number]'
```

### 1.6 Enum

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
console.log(c) // 1

// 默认是从0开始编号的 我们也可以手动修改成员你的数值
enum Colort {Red=1, Green=4, Blue=5}
let a:Colort = Colort.Green
let x : string = Colort[4]
console.log(x) // Green 我们可能想知道这个值映射的是哪个可以直接找


// 性别例子
enum Gender{
    Male=0,
    FaMale=1
}
let d :{name:string,gender:Gender} // 因为存储 男女这种文字是比较占内存的，但是设置成0或者1别人可能看不懂 所以写一个这种枚举类Gender一下就知道了 它会自动映射你是0或者1
d = {name:'dmy',gender:Gender.Male}

if(d.gender === Gender.Male){
    console.log('...')
}
```

### 1.7 Unknown

```typescript
/*
	当我们在写应用的时候可能会需要描述一个我们还不知道其类型的变量。这些值可以来自动态内容，例如从用户获得，或者我们想在我们的 API 中接收所有可能类型的值。在这些情况下，我们想要让编译器以及未来的用户知道这个变量可以是任意类型。这个时候我们会对它使用 unknown 类型。
*/
let un1 : unknown = 1
console.log(un1) // 1
un1 = 'abcdef'
console.log(un1) // abcdef
un1 = true
console.log(un1) // true

// unknown 这个类型的值 是无法赋值给别的类型的 正好与any相反
```

### 1.8 any

```typescript
/*
	有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。 那么我们可以使用any类型来标记这些变量：
*/
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean

/*
	在对现有代码进行改写的时候，any类型是十分有用的，它允许你在编译时可选择地包含或移除类型检查。 你可能认为Object有相似的作用，就像它在其它语言中那样。 但是Object类型的变量只是允许你给它赋任意值 - 但是却不能够在它上面调用任意的方法，即便它真的有这些方法：
*/
let notSure: any = 4;
notSure.ifItExists(); // okay, ifItExists might exist at runtime
notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)

let prettySure: Object = 4;
prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.

// 对于一个数组中想放入很多不同类型的值
let arr1:any[] = [1,'222',true] // any[]  数组中可以是任何类型
for(let i of arr1){
    console.log(i)
}

// 类型为any的变量 可以赋值给任何类型
```

### 1.9 null 和 undefined 和 void

```typescript
// 这两个都有各自的类型为 null 和 undefined 类型
let u : null = null
let n : undefined = undefined
// 声明这两种类型的时候 只能是它们自己 或者是any的时候可以接收
let arr1 : any[] = [1,undefined,null]

// void 经常用于定义一个没有返回值的函数
function a():void{
    console.log('hello')
}
```

### 1.10 never

```typescript
/*
	never类型表示的是那些永不存在的值的类型。 例如，never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是never类型，当它们被永不为真的类型保护所约束时。
*/
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```

### 1.11 object

```typescript
let a :object; // 这种开发里很少用

let b : {
    name?: string,
    age?: number
}

b = {name:'dmy'} // ok
b = {name:'dmy',age:11} // ok
b = {} // ok  在属性名后面接一个?说明是可选的


// 2. props
// 在开发中 我们也许不会将所有的参数定义出来，只需要那么几个但是又不限制在使用函数时传入必须的参数之外的参数

let c : {name:string,[propsName:string]:any} // 这里表示你必须传入一个name 之后你传入的属性都要string并且值是any
c = {sss:111,name:'aa'} // ok
// c = {sa:111}  error

// 3.function
let fn:(a:number,b:number)=>number // 这里表示 你之后给这个fn定义函数的时候 必须是两个参数 a,b 并且都是数值 而且返回值必须是number类型
fn = function(a:number,b:number){
    return 1
}
```



### 1.12 类型断言

```typescript
/*
	有时候你会遇到这样的情况，你会比TypeScript更了解某个值的详细信息。 通常这会发生在你清楚地知道一个实体具有比它现有类型更确切的类型。
	通过_类型断言_这种方式可以告诉编译器，“相信我，我知道自己在干什么”。 类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。 它没有运行时的影响，只是在编译阶段起作用。 TypeScript会假设你，程序员，已经进行了必须的检查。
*/
let someValue : any = 'abcd'
let strlength : number = (<string>someValue).length;

// 使用as
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

### 1.13 类型别名

```typescript
// 1. 对于比较复杂的要经常复用的类型应该怎么办？
let a : 1|2|3|4|5
let b : 1|2|3|4|5
// 这样一遍遍的写非常麻烦

type myNumber = 1|2|3|4|5
let a : myNumber // 这样a的类型就定义好了
a = 6 // error
a = 5 // ok
```

### 1.14 ts文件编译选项

```typescript
// 1. 自动编译
tsc xxx.js -w // 这样只会对xxx这个ts文件进行监视

// 2.tsc命令
// 执行这个命令的前提是你的文件中又tsconfig.json配置文件 之后你执行会对所有的ts文件进行编译
// tsc -w 也会进入监视模式 这回监视的是所有的ts文件
// 必须进入到tsconfig.json这个目录中进行命令的执行


// 配置
include:{ // 开发中不一定所有的ts文件都要编译 这个是配置编译哪个文件夹
    "./src/**/*" // 根目录下src文件夹下的任意文件夹下的任意文件
}
exclude:{ // 开发中不去编译的文件夹
    '....'
}
compilerOptions:{
    target:'es5', // 指定ts文件被编译为什么版本的js
    module:'es2015' // 指定模块要编译为什么版本的 就是导出导入这些
    // lib:[] // 指定库 这个一般不会动都是注掉的 因为有默认值
    outDir: './dist' // 指定编译好的文件放哪 也可以将多个ts文件 编译为一个js './dis/app.js'用的不多
    allowJs: true // 是否在编译的时候也编译js文件,
    checkJs:true // 是否检查js中的语法 这个和上面那个一起使用
    removeComment: true // 是否在编译的时候去除ts中的注释
    noEmitOnError: true // 如果ts中语法有错误则不会进行编译直接报错避免错误的代码放入js中
    alwaysStrict:false // 编译后的JS文件是否使用严格模式 “严格模式性能会更高”默认不开启 如果你的ts代码中有导入导出代码那么你再编译ts 就不会在首行加入 'use strict' 会自动有严格模式
    noImplicitAny:true // 不允许隐式的any出现 比如一个函数接收两个参数 这两个参数你都没有指定类型或者你指定了any类型 是会报错的
    noImplicitThis:true // 不允许不明确的this 比如一个函数 function(){console.log(this)} 这时候我们根本不知道this是谁 你也可以给这个函数一个形参this:any这样就不会报错了
    stricNullChecks: true // 严格检查空置 比如我们在代码中想操作dom但是我们获取的dom可能是不存在的 这里为false的时候是不报错的 开启的话 如果找不到这个dom 就会报错
}
```



### 补充

```typescript
// 1.自动检测
let a:boolean = true
a = 123 // error!

let a = true
a = 123 // error!  这是因为在声明变量和赋值的时候 ts会自动检测类型

// 2.或
let a: string | number;
a = 'hello' // ok
a = 123 // ok
a = true // error

let a : 'hello' | 123;
a = 'hello' // ok
a = 123 // ok
a = 456 // error
a = 'aaa' // error

// 3.与
let b : string & number // 这样写没有意义 因为没有一个值即是字符串又是数字
let b : {name:string} & {age:number}
b = {name:'dmy'} // error
b = {name: 'dmy', age:11} // ok
```



## 2.接口

### 2.1 接口初探

```typescript
function printLabel(labeledObj: { label: string }) {
  console.log(labeledObj.label);
}
let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
// labeledObj: {label:string} 说明你需要传入一个参数为label类型为string的参数 并且我们一般会传入很多的参数但是只要其中有一个符合我们的要求即可

// 使用接口来描述
interface LabeledValue {
  label: string;
}
function printLabel(labeledObj: LabeledValue) {
  console.log(labeledObj.label);
}
let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
/*
	LabeledValue接口就好比一个名字，用来描述上面例子里的要求。 它代表了有一个label属性且类型为string的对象。 需要注意的是，我们在这里并不能像在其它语言里一样，说传给printLabel的对象实现了这个接口。我们只会去关注值的外形。 只要传入的对象满足上面提到的必要条件，那么它就是被允许的。
*/
```

### 2.2 可选属性(略懂)

```typescript
/*
	接口里的属性不全都是必需的。 有些是只在某些条件下存在，或者根本不存在。 可选属性在应用“option bags”模式时很常用，即给函数传入的参数对象中只有部分属性赋值了。
*/
interface  SquareConfig{
    color?: string
    row?: number
}

function createsquare(config:SquareConfig): {color: string; row: number}{ // 这里给这个函数定义了一个返回值 {color:string;row:number} 要以这个类型进行返回
    let newsquare = {color:'white',row:2}
    if(config.color){
        newsquare.color = config.color
    }
    if(config.row){
        newsquare.row = config.row
    }
    return newsquare
}
console.log(createsquare({color:'red'})) // {color:'red',row:2}

/*
	可选属性的好处之一是可以对可能存在的属性进行预定义，好处之二是可以捕获引用了不存在的属性时的错误。 比如，我们故意将createSquare里的color属性名拼错，就会得到一个错误提示
*/
```

### 2.3 只读属性

```typescript
// 有些对象只能在刚刚创建的时候来定义值 之后是不允许修改的 使用关键字 readyonly
interface Point {
  readonly x: number;
  readonly y: number;
}
let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!

/* TypeScript 具有ReadonlyArray<T>类型，它与Array<T>相似，只是把所有可变方法去掉了，因此可以确保数组创建后再也不能被修改 */
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error!

// 上面代码的最后一行，可以看到就算把整个ReadonlyArray赋值到一个普通数组也是不可以的。 但是你可以用类型断言重写：

a = row as number[]

// 对于readonly和const来说 如果是属性则用readonly 若是变量则用const
```

### 2.4 实现接口

```typescript
// 接口中的属性和方法，是没有实际的东西的
interface myType {
    name:string,
    age:number,
    sayHello():void
}
    
// 实现接口使用 implements关键字
class myType1 implements myType{
    name:string
    age:number
    constructor(name:string,age:number){
        this.name = name
        this.age = age
    }
    sayHello(){
        console.log('实现接口把')
    }
}
// 接口其实就是限制这个类的 它和抽象类非常像，就是那个abstract class那个，但是抽象类中可以有不强制子类去写的，但是这个接口就是里面所有的东西以后的类必须都要写
```



## 3.面向对象

### 3.1 基本使用

```typescript
class Person{
    name:string = 'dmy';
    static age : number = 11; // 用static关键字创建的是类属性 无法通过实例进行访问 只能 Person.age 才行 per.age会报错
    readonly address: string = '天津市' // 实例可以访问的只读属性无法修改
    static sayHello(){
        console.log('大家好啊')
        // 如果方法也以static 就是静态方法 只可以直接通过类去调用
    }
}

let per = new Person
console.log(per) // {name:dmy,address:'天津市'}
// console.log(per.age,per.name)
console.log(Person.age) // 11
```

### 3.2 构造函数

```typescript
// constructor的使用
class Dog{
    name:string
    age:number
    constructor(name:string,age:number){
        this.name = name;
        this.age = age
    }
    bark(){
        console.log(this) // 哪个对象调用的 就打印哪个对象的this
    }
}
var doga = new Dog('旺财',11)
```

### 3.3 继承

```typescript
// 秉着一个原则，原始的类不可以随便修改，可以继承然后添加一些东西不要修改源码
// constructor的使用
class Dog{
    name:string
    age:number
    constructor(name:string,age:number){
        this.name = name;
        this.age = age
    }
    bark(){
        console.log(this) // 哪个对象调用的 就打印哪个对象的this
    }
}
var doga = new Dog('旺财',11)


// Cat继承Dog类中的属性以及方法
class Cat extends Dog{
    catSayHello(){ // Cat继承Dog 并且Cat写一个自己的方法
        console.log(`hello我的名字是${this.name}`)
    }
    // 如果父类中的方法不能满足你，那么我们可以重写它
    bark(){
        console.log('我重写了父类中bark方法')
    }
}

let cat1 = new Cat('aa',11)
cat1.catSayHello() // hello我的名字是aa

// super的使用
class Bird extends Dog{
    address:string
    constructor(address:string,name:string,age:number){
        super(name,age) // 如果子类中你想要重写这个构造函数那么你必须执行一个super()并且传入父类需要的形参，这里形参就是name,age
        this.address = address
    }
}
let bird1 = new Bird('地址','名字',11)
```

### 3.4 抽象类

```typescript
// 有一种类就是专门被人继承的比如动物，我们不想别人直接用它来创建类，只允许利用它继承
abstract class Animal{
    name:string;
    age:number;
}
// 抽象类就是在前面加入一个abstract关键字

// 抽象方法
// 有一种方法，比如sayHello我们希望下面的每个子类都有这个方法但是父类中又不能明确写出这个方法的实现比如猫也又这个就是打印你好我是猫，狗就是你好我是狗，但是父类中无法明确的写出实现过程所以我们可以写一个抽象方法，抽象方法就是父类中定义好这个模板，以后所有的子类必须重写这个方法
abstract class Animal{
    name:string;
    age:number;
    abstract sayHello():void // 模板，返回空，子类必须重写它，否则报错
}
```

## 4 属性得封装

```typescript
// 1. public 公有属性，任何地方都可以访问或者修改该属性
// 2. private 私有属性，只有这个类才可以，外部和子类都无法访问和修改
// 3. protected 保护属性，只有这个类和子类可以访问到，外部无法访问

// 例子
class Person{
    public name:string 
    private _age:number
    constructor(name:string,age:number){
        this.name = name
        this._age = age
    }
    // 非ts
    /*
    getAge(){
        return this.age
    }
    setAge(value:number){
        if(value<=0){
            throw console.error('年龄不可以小于0');
        }else{
            this.age = value
        }

    }
     */
    // ts
    get age(){
        return this._age
    }
    set age(value:number){
        this._age = value
    }

}

let peron = new Person('dmy',18)
// console.log(person.age) error 只能在类内部访问
console.log(peron.age) // 这就相当于调了get age那个获取age得值
peron.age = 11 // 这里相当于调了 set age
console.log(peron.age)

class A{
    protected num:number
    constructor(num:number){
        this.num = num
    }
}
class B extends A{
    sayNum(){
        console.log(this.num)
    }
}

let bba = new B(1)
// bba.num  error
```

## 5 泛型

```typescript
// 泛型，就是说我们不知道是什么类型，T就是泛型，A函数需要一个参数a,这个a会根据你调用这个函数得时候，使这个泛型具有类型
function A<T>(a:T):T{
    return a
}

A<string>('123') // <string> 就是指明了该泛型就是一个string类型
A<number>(123) // ok
A(123) // ok
A(true) // ok


interface myinter{
    length:number
}
// 泛型B 必须实现接口myinter
function B<B extends myinter>(b:B){
    return b
}

// B(123)  error 因为数字是没有 length这个属性得
B('123') // ok 字符串有length

B({length:123}) // ok 设置一个对象里面有length也可以


// 泛型应用到类中
class Myclass<T>{
    name:T
    constructor(name:T){
        this.name = name
    }
}

let class1 = new Myclass<string>('123') // ok
let class2 = new Myclass(123) // ok
```

## 6.项目练习

j
