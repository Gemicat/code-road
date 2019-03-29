# Promise、async、await执行顺序 {docsify-ignore-all}

```js
async function async1() {
    console.log("async1 start");
    await async2()
    console.log("async1 end");
};

async function async2() {
    console.log("async2 start");
    await async3();
    console.log("async2 end");
};

async function async3() {
    console.log("async3 start");
};

setTimeout(function () {
    console.log('setTimeout0');
}, 0);

console.log("start");

async1();

new Promise(function (resolve) {
    console.log("Promise1");
    resolve();
}).then(function () {
    console.log("Promise2");
});

console.log("all end");
```

## async

> async function 声明将定义一个返回 AsyncFunction 对象的异步函数。当调用一个 async 函数时，会返回一个 Promise 对象。当这个 async 函数返回一个值时，Promise 的 resolve 方法会负责传递这个值；当 async 函数抛出异常时，Promise 的 reject 方法也会传递这个异常值。

所以你现在知道咯，使用 async 定义的函数，当它被调用时，它返回的其实是一个Promise对象。
我们再来看看 await 表达式执行会返回什么值。

## await

> async 函数返回一个 Promise 对象，当函数执行的时候，一旦遇到 await 就会先返回，等到触发的异步操作完成，再接着执行函数体内后面的语句。

所以，当await操作符后面的表达式是一个Promise的时候，它的返回值，实际上就是Promise的回调函数resolve的参数。

明白了这两个事情后，我还要再啰嗦两句。我们都知道Promise是一个立即执行函数，但是他的成功（或失败：reject）的回调函数resolve却是一个异步执行的回调。当执行到resolve()时，这个任务会被放入到回调队列中，等待调用栈有空闲时事件循环再来取走它。

**参考资料：**

[promise、async和await之执行顺序的那点事](https://lvdingjin.github.io/tech/2018/05/27/async-and-await.html)