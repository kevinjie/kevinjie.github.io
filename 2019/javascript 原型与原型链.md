# javascript 原型与原型链



* 构造函数创建对象

我们都知道，JS中可以通过构造函数创建对象
```js
function Mobile() {};
var iphone = new Mobile();
```
Mobile 就是一个构造函数（首字母大写），iphone就是构造函数创建的一个对象。

* prototype

每一个函数都有一个prototype属性，那么这个prototype到底是指的什么？其实prototype指向的是一个对象，这个对象就是构造函数创建对象的原型。
```js
Mobile.prototype
  {constructor: ƒ}
    constructor: ƒ Mobile()
    __proto__: Object
```

* __proto__

每个除了null以外的JS对象都有__proto__属性，绝大多数浏览器都支持通过__proto__这个非标准的属性访问原型，也就是说实例对象的__proto__属性就是构造函数的prototype
```js
Mobile.prototype === iphone.__proto__ // true
```


* constructor

既然实例对象和构造函数都有属性指向原型对象，那么原型对象有没有属性指向实例和构造函数呢？答案是，原型对象是没有属性指向实例的，实例太多了。原型对象中的constructor指向关联的构造函数
```js
Mobile.prototype.constructor === Mobile // true
```

* 实例与原型

如果要获取实例中的某个属性，首先会尝试到实例中获取，如果实例中没有，就会去实例的原型中获取，如果原型中没有，就会去原型的原型中获取，一直找到最顶层为止


* 原型的原型

那么原型的原型到底是什么？原型也是一个对象，那么就有__proto__属性，那么我们就可以通过__proto__获取原型的原型
```js
Mobile.prototype.__proto__
  constructor: ƒ Object()
```
Mobile.prototype的原型的constructor是Object，由此可知Mobile.prototype.__proto__是Object()构造函数的原型对象那么Object.prototype.__proto__又是什么呢？是null，就是没有值的意思
```js
Object.prototype.__proto__ // null
```
* 原型链

由以上可知，由对象的__proto__构成的一个链条就是所谓的原型链
```js
Mobile.prototype.__proto__.__proto__
```


