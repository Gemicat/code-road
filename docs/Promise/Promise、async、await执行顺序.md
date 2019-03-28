# Promise、async、await执行顺序

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

**参考资料：**

[promise、async和await之执行顺序的那点事](https://lvdingjin.github.io/tech/2018/05/27/async-and-await.html)