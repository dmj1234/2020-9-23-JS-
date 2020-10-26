### 构造函数就是能够构造出一个对象来。

所有js中的函数从出生就自带一个prototype的属性，prototype从出生就自带一个constructor，constructor从出生时它的值就是函数自身。

function f1（）{}
f1.prototype.constructor===f1

也就是 函数.prototype.constructor===函数



### 关于「原型」

每个对象都有原型，除了根对象 Object.prototype 比较特殊，原型为 null
一个对象的原型指的是这个对象与其他同类对象的公有属性的集合，比如 obj1 和 ob2 同时拥有 toString / valueOf，那么 toString / valueOf 等属性组成的对象，就是 obj1 和 obj2 的原型
一个对象的原型的地址存在这个对象的 __proto__ 属性里，比如 obj1 的原型地址就存在 obj1.__proto__
obj1.__proto__和 Object.prototype 都存储着 obj1 原型的地址
当我们说「obj1 的原型」时等价于说「obj1.__proto__」




### 关于 prototype 属性

所有函数一出生就有一个 prototype 属性
所有 prototype 一出生就有一个 constructor 属性
所有 constructor 属性一出生就保存了对应的函数的地址
如果一个函数不是构造函数，它依然拥有 prototype 属性，只不过这个属性暂时没什么用


new X() 操作其实自动帮我们做了很多事情

自动创建一个空对象
自动将该空对象的原型指向 X.prototype（即将 X.prototype 保存的地址复制到空对象.__proto__ 里）
自动将空对象作为 this 来运行构造函数
自动 return this
构造函数X

x函数本身负责给对象本身添加属性
2. x.prototype负责保存对象的共有属性



### 类型 和 类 的描述中

类型是对 JS 中数据的分类
类是对 JS 中对象的分类
JS 中的类型有：数字、字符串、布尔、符号Symbol、null、undefined、对象
JS 中的类有：对象 Object、数组 Array、函数 Function 等


### 关于 Object.prototype



是一个对象（这么说不严谨，应该说 Object.prototype 保存着一个对象的地址），包含了 toString、valueOf、hasOwnProperty 等对象共有的属性
Object 的原型是指 Object.__proto__，不是 Object.prototype，因为 Object.prototye 是 Object 构造出来的对象的原型
Object.prototype 是所有对象的原型（除了它自己），但 Object.prototype 有可能不是第一层原型，而是第二层原型，比如 arr 的第一层原型是 Array.prototype，第二层原型才是 Object.prototye
Object.prototype 自己的原型为 null


JS 构造对象目前有两种方式，一种是用构造函数+prototype，一种是用 class，关于这两种方式，

两者方式 JS 都支持，JS 是一门包容的语言，提供了多种表达形式，两者方式都能表达程序员的思想。
构造函数+prototype 是先提供的，class 是后提供的，说明 构造函数+prototype 是 JS 一开始的基因，而 class 的粉丝其实更喜欢 class，所以两种都有必要学习


### 构造函数+prototype

function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHi = function() {
  console.log("你好，我叫" + this.name);
};

let person = new Person("frank", 18);
let person2 = new Person("jack", 19);



class 方式

class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  sayHi() {
    console.log("你好，我叫" + this.name);
  }
}
let person = new Person("frank", 18);
let person2 = new Person("jack", 19);

代码规范

大小写

所以构造函数（专门用来创建对象的函数）首字母大写
所有被构造出来的对象，首字母小写
词性

函数名称一般用动词
new后面的函数用名词


如何确认一个对象的原型

结论：你是谁构造的，你的原型就是谁的prototype属性对应的对象

原型公式：对象.__ proto __===其构造函数.prototype



终极一问

window是谁构造的

答案：Window（大写）

window.Object是谁构造的

答：window.Function（所有函数都是window.Function构造的）

window.Function是谁构造的

答：是他自己（其实是浏览器够早了它，然后指定是他自己构造了自己