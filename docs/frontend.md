# CSS 疑惑

- CSS px 和 viewport 是怎么样的？
- CSS 中的子元素中的百分比（%）到底是谁的百分比？

> 参考：[响应式布局的常用解决方案对比(媒体查询、百分比、rem和vw/vh）](https://github.com/forthealllight/blog/issues/13)

## CSS

### BFC margin 塌陷、折叠



# JS 语法碎片

## ECMAScript 6

>[Babel](https://babeljs.io/)
>关于ES5严格模式，[MDN Strict_Mode](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)

### 变量声明：const/let

- 之前：var命令会发生“变量提升”现象，即变量可以在声明之前使用，值为undefined
- let/const带来的新特性：块级作用域、不具备变量提升
- let一般用于声明一个值会改变的量，const一般用于声明一个常量
- const声明一个只读的常量。一旦声明，常量的值就不能改变。
- const不保证指向的数据结构是不是可变的，可保证简单类型的数据（数值、字符串、布尔值）不可变
- 块级作用域解决的问题
  - 避免内层变量覆盖外层变量
  - 避免计数的循环变量泄露为全局变量

```js
//干掉变量提升
console.log(foo);//undefined
var foo = 2;

console.log(bar);//ReferenceError
let bar = 2;

//----------------------------------------
var tmp = 123;

if (true) {
    tmp = 'abc'; // ReferenceError
    let tmp;
}

//内层变量覆盖全局变量
var tmp = new Date();

function f() {
    console.log(tmp);
    if (false) {
        var tmp = 'hello world';
    }
};

f();//undefined

//计数的循环变量泄露为全局变量
var s = 'hello';

for (var i = 0; i < s.length; i++) {
    console.log(s[i]);
}

console.log(i);//5
```

### 箭头函数

- 箭头函数不需要参数或需要多个参数，使用一个圆括号包围参数部分
- 箭头函数可以替换函数表达式，但是不能替换函数声明
- **箭头函数中，没有this。如果在箭头函数中使用了this，那么该this一定就是外层的this**
- 箭头函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象
- 箭头函数的this对象是固定的

```js
//ES6
(x, y, z) => x+y+z;
//ES5, Babel转换后
"use strict";

(function (x, y, z) {
    return x + y + z;
});

//ES6
var foo = (x, y, z) => x+y+z;
//ES5
"use strict";

var foo = function foo(x, y, z) {
    return x + y + z;
};
```

在ES6中，会默认采用严格模式，使用箭头函数时需要慎重使用**this**

```js
//https://es6.ruanyifeng.com/#docs/function#%E4%B8%8D%E9%80%82%E7%94%A8%E5%9C%BA%E5%90%88
const Person = {
    name: 'yeshan',
    getName: () => this.name,//this并非指向Person
};

//Babel编译后
"use strict";

var _this = void 0;

var Person = {
    name: 'yeshan',
    getName: function getName() {
        return _this.name;
    }
};

//--------------------------------------
//阔以这么操作
const person = {
    name: 'yeshan',
    getName: function() {
        return () => this.name
    }
}
//Babel后
"use strict";

var person = {
    name: 'yeshan',
    getName: function getName() {
        var _this = this;
        return function () {
            return _this.name;
        };
    }
};
```

- [箭头函数不适用场合](https://es6.ruanyifeng.com/#docs/function#%E4%B8%8D%E9%80%82%E7%94%A8%E5%9C%BA%E5%90%88)

### 解析结构

```js
const arr = [1, 2, 3];
const [a, b, c] = arr;

a//1
b//2
c//3

//对象的解析
const props = {
    className: 'tiger-button',
}

const {className} = props

//Babel后
"use strict";

var props = {
    className: 'tiger-button'
};
var className = props.className;
```

### 展开运算符

- 展开语法(Spread syntax), 可以在函数调用/数组构造时, 将数组表达式或者string在语法层面展开；还可以在构造字面量对象时, 将对象表达式按key-value的方式展开。
- 可用于将已有数组元素变成新数组的一部分

```js
//数组展开
var parts = ['shoulders', 'knees'];
var lyrics = ['head', ...parts, 'and', 'toes'];
lyrics//["head", "shoulders", "knees", "and", "toes"]

//函数不定参，只能放最后
//https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Rest_parameters
const add = (a, b, ...more) => {
    return more.reduce((m, n) => m + n) + a + b
}
console.log(add(1, 23, 1, 2, 3, 4, 5))//39

//对象展开
//对象的mixin模式：https://es6.ruanyifeng.com/#docs/class-extends#Mixin-%E6%A8%A1%E5%BC%8F%E7%9A%84%E5%AE%9E%E7%8E%B0
var obj = { foo: 'bar', x: 42 };
var clone_obj = {...obj};
clone_obj//{foo: "bar", x: 42}
```


- [MDN展开语法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

### 对象字面量

- [https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types#%E5%AF%B9%E8%B1%A1%E5%AD%97%E9%9D%A2%E9%87%8F(Object_literals)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types#%E5%AF%B9%E8%B1%A1%E5%AD%97%E9%9D%A2%E9%87%8F(Object_literals))
- [https://mp.weixin.qq.com/s/NnjGk8yO7snSGBUTT7pjIQ](https://mp.weixin.qq.com/s/NnjGk8yO7snSGBUTT7pjIQ)

### 面向对象

#### ES6面向对象

- 类和模块的内部，默认为严格模式，所以不需要使用use strict指定运行模式
- 类的所有方法都定义在类的prototype属性上面
- ES6中，类的内部所有定义的方法，都是不可枚举的（non-enumerable）
- 一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被默认添加，有点像CPP
- 类必须使用new调用

```js
class Complex {
    constructor(r, img) {//构造方法
        this.image = img;//实例this上的属性
        this.real = r;
    }

    print() {
        console.log(this.real + '+' + this.image + 'i');
    }

    toString() {//原型对象上的属性，定义在类上
        return '(' + this.real + ', ' + this.image + ')';
    }
}

let c = new Complex(1,2);
c.print();//12
console.log(c.hasOwnProperty('image'));//true
console.log(c.__proto__.hasOwnProperty('image'));//false
console.log(Complex.hasOwnProperty('image'))//false;
console.log(c.hasOwnProperty('print'));//false
console.log(c.__proto__.hasOwnProperty('print'));//true
console.log(c.__proto__==Complex)//false
```

实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。

**类的方法内部如果含有this，它默认指向类的实例。但是，必须非常小心，一旦单独使用该方法，很可能报错。**，[this的注意点](https://es6.ruanyifeng.com/#docs/class#%E6%B3%A8%E6%84%8F%E7%82%B9)。

#### 理解原型链

```js
function Person(){
}

var person = new Person();//person 为实例

console.log(Person === person.constructor);//true
console.log(Person.prototype.constructor.name)//"Person"
```

Person.prototype 与 person.__proto__

![实列](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200720235410.png)

![原型链](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200720235239.png)

##### 类的继承

- 使用extends进行类继承
- **子类必须在constructor方法中调用super方法，否则新建实例时会报错。**这是因为子类自己的this对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。如果不调用super方法，子类就得不到this对象。
- 如果子类没有定义constructor方法，这个方法会被默认添加

```js
class NewComplex extends Complex {
    constructor(x,y,z) {
        super(x,y);
        this.z = z;
    }

    new_print() {
        console.log(this.z);
    }
}

test = new NewComplex(1,2,3);
test.print();//1+2i
test.new_print();//3
```

#### ES5面向对象

```js
class Complex {
    constructor(r, img) {//构造方法
        this.image = img;//实例this上的属性
        this.real = r;
    }

    print() {
        console.log(this.real + '+' + this.image + 'i');
    }

    toString() {//原型对象上的属性，定义在类上
        return '(' + this.real + ', ' + this.image + ')';
    }
}

let c = new Complex(1,2);
c.print();//12
//-----------------------------------------------------------
//Babel编译后
"use strict";

var Complex =
/*#__PURE__*/
function () {
    function Complex(r, img) {
    //构造方法
        this.image = img; //实例this上的属性

        this.real = r;
    }

    var _proto = Complex.prototype;

    _proto.print = function print() {
        console.log(this.real + '+' + this.image + 'i');
    };

    _proto.toString = function toString() {
        //原型对象上的属性，定义在类上
        return '(' + this.real + ', ' + this.image + ')';
    };

    return Complex;
}();

var c = new Complex(1, 2);
c.print(); //12
```

### 模块module


- export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系。
- export语句输出的接口，与其对应的值是**动态绑定关系**，即通过该接口，可以取到模块内部实时的值
- import命令大括号里指定的从其他模块导入的变量需要与被导入模块对外接口的名称相同
- 建议凡是输入（import）的变量，都当作完全只读，不要轻易改变它的属性。
- export default命令用于指定模块的默认输出。**一个模块只能有一个默认输出**，因此export default命令只能使用一次。所以，import命令后面不用加大括号，因为只可能唯一对应export default命令。

```js
//xxx.js
var name = 'yeshan';
export { name };
export { xx as name};//as关键字重命名

function f() {}
export { f };

class H {}
export default H;

//call.js
import {name} from 'xxx.js'
```

- [ES6 模块与 CommonJS 模块的差异](https://es6.ruanyifeng.com/#docs/module-loader#ES6-%E6%A8%A1%E5%9D%97%E4%B8%8E-CommonJS-%E6%A8%A1%E5%9D%97%E7%9A%84%E5%B7%AE%E5%BC%82)
- [模块的整体加载](https://es6.ruanyifeng.com/#docs/module#%E6%A8%A1%E5%9D%97%E7%9A%84%E6%95%B4%E4%BD%93%E5%8A%A0%E8%BD%BD)

### Nullish Coalescing、Optional Chaining

空值合并操作符（??）是一个逻辑操作符，当左侧的操作数为 null 或者 undefined 时，返回其右侧操作数，否则返回左侧操作数

```javascript
const foo = null ?? 'default string';
console.log(foo);
// expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// expected output: 0
```

可选链操作符( ?. )允许读取位于连接对象链深处的属性的值，而不必明确验证链中的每个引用是否有效。?. 操作符的功能类似于 . 链式操作符，不同之处在于，在引用为空(nullish ) (null 或者 undefined) 的情况下不会引起错误，该表达式短路返回值是 undefined。

```javascript
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah'
  }
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// expected output: undefined

console.log(adventurer.someNonExistentMethod?.());
// expected output: undefined
```

- [Nullish Coalescing](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)
- [Optional Chaining](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/%E5%8F%AF%E9%80%89%E9%93%BE)