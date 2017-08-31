### 什么是 ES6 ？
ES 是 JavaScript 的背后的标准名。ES6 是 JS 的新标准，目前人们提到 ES6 指的就是“新 JS” 。

ES6 的功能，浏览器只能大部分支持，所以如果我们在开发的时候，用到 ES6 ，那么一定涉及到一个编译的概念。更准确的说法叫”预处理“或者””转译“（因为整个过程就是把 ES6 转换为老 JS 语法，保证浏览器可以支持）。

ES6 就是一套新 JS 语法的总和

具体涉及到哪些功能，可以参考：

http://es6.ruanyifeng.com/
如何”转译“ ES6 ？

使用 Babel 来进行转译。可以到 https://babeljs.io/ 去试用一下 babel 。但是，实际开发中，我们都是在命令行中去自动化的使用 Babel 。

Babel 的官网在：http://babeljs.io/ 。官网上对它的描述是：

一个 Javascript 的编译器( compiler )

我们知道的 create-react-app 这个开发环境，其中就集成了 Babel 。

为何要使用 ES6 ？

第一，好用。

第二，大家都用。你不用你就 OUT 。

### 什么是面向对象编程？
Object Oriented Programming 面向对象编程

参考：http://haoqicat.com/o-o-js

基本概念：面向对象编程，是一种基于 对象 这个概念的编程方法论。对象中 可以包含数据，一般被成为属性 ，也可以包含函数，一般被成为方法。

OOP: 类和对象

类（ class ）是多个对象（ object ）的抽象，对象是类的实例。人，就可以是一个类，比如人可以有名字，身高这些属性，但是没有具体值，所以说类可以理解为一个空的木桶。 对象是类的实例，具体的一个人，就可以叫做

人这个类的一个对象

例如，Peter 就可以是人这个类的一个对象。对象的特点是有具体数据的，例如，给定一个人 Peter ，那我们可以得到他的具体的姓名，身高的具体值。所以对象可以理解为木桶中装的水。

动手

下面用代码的形式来表述一下类和对象的关系。在面向对象编程的过程中，我们都是先定义类

class Person {
  constructor(name) {
    this.name = name;
  }
}
class 关键字是 ES6 的新特性。上面 name 就是一个属性 ，constructor() 是一个方法。

有了类之后，我们就可以实例化出，无穷多个对象了

let peter = new Person('happypeter');

console.log(peter.name);
上面 new 是一个关键字，意思是“新建一个该类的实例” 。得到的 peter 就是一个对象（就是类的实例），我们可以得到 peter 中的 name 的具体值。

constructor 构造函数

构造函数也是面向对象编程的一个术语。

一个类里面可以定义多个方法，如下

class Person {
  constructor() {
    console.log('hello1');
  }
  sayHello2() {
    console.log('hello2');
  }
}
let peter = new Person;
上面 constructor 是一个特殊的方法（拼写是严格的），它的特点是在对象 被创建的时候，也就 let peter = new Person 这一句执行的时候，自动被 呼叫的一个方法。而其他的方法，都不会被自动执行。

注： constructor 的英文本意：构造者。

同时，constructor 也可以接受参数，如下

class Person {
  constructor(name) {
    console.log('My Name is ' + name);
  }
}
let peter = new Person('peter');
如上，给 constructor 传递参数的方式，就是在 new 一个新对象的时候，在 类名之后直接加括号来传递，例如 Person('peter') 。

定义自己的方法

constructor 是一个特殊的方法，它的拼写就是 constructor ，拼错了，就不会 被自动执行了。或者说，就成了一个普通方法了。通常我们的类里面都会定义很多普通 方法的。

class Person {
  sayHello(name) {
    console.log('hello ' + name);
  }
}
let peter = new Person;
那么创建新对象的时候，sayHello 是不会被自动执行的，那么如何来调用呢？

peter.sayHello('lily');
this 关键字

this 指的就是当前对象

class Person {
  constructor(name) {

  }
  sayName() {
    console.log('my name is' + name);
  }
}
let peter = new Person('peter');
peter.sayName();
此时如果直接看 peter.sayName() 会发现 name 的值为空。

解决这个问题就可以使用 this 关键字。

class Person {
  constructor(name) {
    this.name = name;
  }
  sayName() {
    console.log('my name is' + this.name);
  }
}
let peter = new Person('peter');
peter.sayName();
这样 sayName() 函数中就可以拿到 this.name 的值了。

出一个题

我们来构造一个类，叫 Dog 。然后 new 一个对象，叫 doudou ，要求

doudou.sayName()
# 输出 doudou
运行环境使用 nodejs 。

答案是：

class Dog {
  constructor (name) {
    this.name = name
  }
  sayHello () {
    console.log(this.name)
  }
}

let doudou = new Dog('doudou')
let feifei = new Dog('feifei')
doudou.sayHello()
feifei.sayHello()
### 如何使用类的继承？
类的继承也是面向对象编程的基本知识。

比如人是一个类

class Person {
  sayKind() {
    console.log('I am human');
  }
}
人的基础之上男人又形成一类

class Men {
  sayGender() {
    console.log('Male');
  }
}
其实我们可以采用继承的方式，让 Men 中可以拥有 Person 中的属性和方法。

代码

class Person {
  sayKind () {
    console.log('human')
  }
}

class Men extends Person {
  sayGender () {
    console.log('Male')
  }
}

class Women extends Person {
  sayGender () {
    console.log('Female')
  }
}


const peter = new Men
const billie = new Women
peter.sayKind()
billie.sayKind()
概念

上面代码中，父类是 Person ，子类就是 Women 和 Men 。extends 英文本意是拓展 ，这里基本就是继承的意思。
### super（）是干嘛的？
super() 方法在类继承中的作用

我们现在来看，既然方法可以被继承，那么属性当然也应该是可以被继承的。

class Person {
  constructor() {
    this.weight = "around 100kg";
    this.height = "around 170cm";
  }
}
class Men extends Person {
  constructor() {
    super();
    this.gender = "Male";
  }
}

let peter = new Men;
console.log(peter.weight);
问题是，在上面的代码中，如果没有 super() 调用，那么子类中就不允许使用 this ，报错信息是

repl: 'this' is not allowed before super()
   8 |   constructor() {
   9 |     // super();
> 10 |     this.gender = "Male";
     |     ^
  11 |   }
  12 | }
那么，super() 到底是什么呢？

答案是这个样子的：子类的 this 是基于父类的 this 的（先创建父类的对象，然后再在上面进行增加） ，也就是说在父类对象没有被创建的时候，子类是没有办法被创建的。而 super() 指的就是父类的 constructor() 所以添加了 super() 在子类中，问题就解决了。

经验就是：子类的 constructor() 中必须先呼叫 super() ，然后才能使用 this 。
### ES6 模块怎么用？
模块入门

模块（ module ），基本意思就是把一个大程序，切分成多个文件。这样，说白了，一个文件就是一个模块。但是，在 ES6 编程领域，模块有自己的一些固定的使用语法。

ES6 模块

react 写代码的时候要用 ES6 模块。

es6 module 基本语法如下：

export // (命名导出,默认导出)
import // 导入
ES6 模块到底帮我们解决什么问题

ES6 模块的引入，基于的现实是当前 Web 项目变得复杂了，所以 JS 文件会切分成 不同的多个文件，这样，没有模块之前，我们是使用 <script> 标签来导入多个 js 文件，但是，如果一个 html 文件中有几十个 script 标签来加载 js 文件，那么造成 的问题就是：

会发出多个 http 请求，影响页面加载速度
各个 JS 文件之间的依赖关系混乱，给项目管理带来了困难
于是 ES6 模块就是我们的救星。

模块默认隔离所有内容

隔离：意思就是如果我在当前模块中，声明一个变量或者函数，那么默认其他文件（模块）中是访问不到的。

比如我们有这样的程序

class Person {
  sayHello(){
    console.log('hello');
  }
}
let i = 1;

let peter = new Person;
peter.sayHello();
console.log(i);
是这样，一个文件中我们定义一个变量（或者一个类，函数），那么它的作用范围一般 就是在整个文件内可以用了，这样的好处是使用方便，但是，当程序写大之后，变量名 冲突就会带来调试困难。针对这个问题，ES6 模块的默认行为是隔离，一个变量一旦 移动到模块中，那么即使我们导入模块文件，那么默认情况下，这个变量也不能在模块之外 的位置被访问到。

既然模块中的变量，默认是隔离的，那么就需要我们明文的去进行变量的导出和导入。

导出方式

有两种形式：

第一种叫做默认导出 。用 export default Person; 。对应的导入方式是 import Person from './Person' 。默认导出方式，在一个模块中，只能用一次，同时一次只能导出一个变量。

另一种形式叫做命名导出 。如果我们想要一次导出多个变量，那就 export { Person，i};，对应的导入方式是 import { Person, i} from ./Person ，

理解了导入导出方式，也就掌握了 ES6 模块。

运行环境

import/export 是 ES6 新关键字。普通浏览器包括 nodejs 都还不支持。所以代码未来我们需要到 create-react-app 环境中去使用。
### 为何要发明 let 和 const ？
在老 JS 语法中，也就是 ES5 中，声明变量使用 var 。但是 ES6 中推荐使用 let 和 const 。

var 的缺陷

var 总体来说，就是很烂。毛病有：

作用域不清晰，造成各种尴尬使用情形，具体见下面参考链接
可以重复声明，代码有错误，不容易报错出来
对应 let 和 const 就是避免这些问题。

多说一句：TS（ typeScript ）现在这么火，就是因为强类型，报错多。

let 和 const 的区别

let 用来声明变量 。const 用来声明常量 。let 定义的变量，后续允许修改。const 定义一个变量后，一旦修改就会报错（当然，const 也不是绝对不能改的，详情见参考链接）。

参考

http://es6.ruanyifeng.com/#docs/let
### 解构赋值是什么？
解构赋值，是后续我们开发中非常常用的一种赋值方式。它的特点是简短和易懂，并没有提供什么以前不能完成的功能，所以可以认为是一种语法糖。

比如我有一个对象：

const user = { name: ‘happypeter’, email: 'peter@peter.com', wechat: 'happypeter1983' }

let name = user.name
let email = user.email
let wechat = user.wechat
这样，我们就可以把 obj 中的数据，单独赋值给某个变量来使用了。完全不用依赖于解构赋值。但是，如果用解构，那么语句会简单很多

const { name, email, wechat } = user
数组

数组上也能用。

let [a, b, c] = [1, 2, 3]
参考

http://es6.ruanyifeng.com/#docs/destructuring
### 模板字符串
解构赋值，是后续我们开发中非常常用的一种赋值方式。它的特点是简短和易懂，并没有提供什么以前不能完成的功能，所以可以认为是一种语法糖。

比如我有一个对象：

const user = { name: ‘happypeter’, email: 'peter@peter.com', wechat: 'happypeter1983' }

let name = user.name
let email = user.email
let wechat = user.wechat
这样，我们就可以把 obj 中的数据，单独赋值给某个变量来使用了。完全不用依赖于解构赋值。但是，如果用解构，那么语句会简单很多

const { name, email, wechat } = user
数组

数组上也能用。

let [a, b, c] = [1, 2, 3]
参考

http://es6.ruanyifeng.com/#docs/destructuring
### 胖箭头函数
胖箭头函数（ arrow function ) 是非常常用的。从此我们的函数可以写的更为简短，同时省去了绑定 this 的麻烦。

原本函数我们要写成

const myFun = function (name) {
  console.log(name)
}
现在可以写成

const myFun = (name) => {
  console.log(name)
}

myFun('happypeter')
同时，如果参数只有一个，那么可以把括号去掉，写成

const myFun = name => {
  console.log(name)
}

myFun('happypeter')
同时，如果里面的语句只有一条，那么花括号也可省去。

const myFun = name =>
  console.log(name)

myFun('happypeter')
既然，语句很少，那么写到一行上也可以。

const myFun = name => console.log(name)

myFun('happypeter')
如果，我希望函数最终返回 name 的两倍。那我可以写成

const myFun = name => {
  return name + name
}

console.log(myFun('happypeter'))
但是，箭头函数还有一个好处，默认就 return 最后的那个东西。所以可以写成

const myFun = name => name + name
为何要把函数弄得这么简短

因为 JS 特别强调函数式编程，也就是经常弄一些无名函数，作为另外一个高阶函数的参数，传来传去，那么这样定义函数时语句的简短就显得非常有必要了。

另外一个好处：this 穿透

老的函数写法，需要经常 bind(this) ，因为 this 是不穿透的，箭头函数默认可以让父作用域的 this 直接穿透进来，所以一般不需要 bind(this) 。

参考

http://es6.ruanyifeng.com/#docs/function#箭头函数
http://haoduoshipin.com/v/211.html
