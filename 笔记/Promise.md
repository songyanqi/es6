### Promise  的简单使用方法：
优点：
```Javascript
var pms1 = new Promise(function(resolve, reject) {
    setTimeout(function() {
        console.log('执行任务1');
        resolve('执行任务1成功');
    }, 2000);
});
pms1.then(function(data){ // data 形参 表示 resolve执行成功的里面的 实参
    // 执行下一个任务
}) 

Promise.resolve('foo')
// 等价于
new Promise(resolve => resolve('foo'))
```


# 语法：
new Promise( function(resolve, reject) {...} /* executor */  );

Promise是一个构造函数，自己身上有all、reject、resolve这几个眼熟的方法，
原型上有then、catch等同样很眼熟的方法。

all的用法:
Promise的all方法提供了并行执行异步操作的能力，并且在所有异步操作执行完后才执行回调。


下面代码中，第二种写法要好于第一种写法，理由是第二种写法可以捕获前面then方法执行中的错误，也更接近同步的写法（try/catch）。
因此，建议总是使用catch方法，而不使用then方法的第二个参数。

跟传统的try/catch代码块不同的是，如果没有使用catch方法指定错误处理的回调函数，Promise 对象抛出的错误不会传递到外层代码，即不会有任何反应。
```Javascript
// bad
promise
  .then(function(data) {
    // success
  }, function(err) {
    // error
  });

// good
promise
  .then(function(data) { //cb
    // success
  })
  .catch(function(err) {
    // error
  });
  ```
