### 原始类型有哪几种？null 是对象吗？原始数据类型和复杂数据类型存储有什么区别？

* 原始类型有6种，分别是undefined，null，bool，string，number，symbol(ES6新增)。
* 虽然 typeof null 返回的值是 object，但是null不是对象，而是基本数据类型的一种。
* 原始数据类型存储在栈内存，存储的是值。
* 复杂数据类型存储在堆内存，存储的是地址。当我们把对象赋值给另外一个变量的时候，复制的是地址，指向同一块内存空间，当其中一个对象改变时，另一个对象也会变化。

### typeof null 为什么等于 object？

在 JS 中二进制前三位都为 0 的话会被判断为 object 类型，null 的二进制表示全是 0，自然前三位为 0，和 object 的表现一致。

### typeof 是否正确判断类型? instanceof呢？ instanceof 的实现原理是什么？

首先 typeof 能够正确的判断基本数据类型，但是除了 null, typeof null输出的是对象。

但是对象来说，typeof 不能正确的判断其类型， typeof 一个函数可以输出 'function',而除此之外，输出的全是 object,这种情况下，我们无法准确的知道对象的类型。

instanceof可以准确的判断复杂数据类型，但是不能正确判断基本数据类型。(正确判断数据类型请戳：https://github.com/YvetteLau/Blog/blob/master/JS/data-type.js)

instanceof 是通过原型链判断的，A instanceof B, 在A的原型链中层层查找，是否有原型等于B.prototype，如果一直找到A的原型链的顶端(null；即`Object.prototype.__proto__`),仍然不等于B.prototype，那么返回false，否则返回true.

instanceof的实现代码:

```js
// L instanceof R
function instance_of(L, R) {//L 表示左表达式，R 表示右表达式
    var O = R.prototype;// 取 R 的显式原型
    L = L.__proto__;    // 取 L 的隐式原型
    while (true) { 
        if (L === null) //已经找到顶层
            return false;  
        if (O === L)   //当 O 严格等于 L 时，返回 true
            return true; 
        L = L.__proto__;  //继续向上一层原型链查找
    } 
}
```


> 转自 [【面试篇】寒冬求职季之你必须要懂的原生JS(上)](https://juejin.im/post/5cab0c45f265da2513734390?utm_source=gold_browser_extension)