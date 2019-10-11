### 1、async 关键字的函数 和 普通函数 的区别：
demo：

```javascript

async function fn1(){
    return 123
}

function fn2(){
    return 123
}

console.log(fn1())  // Promise {<resolved>: 123}
console.log(fn2())  // 123

```
### 2、关于async关键字还有哪些要注意的？

在语义上要理解，async表示函数内部有异步操作。
另外注意，一般 await 关键字要在 async 关键字函数的内部，await 写在外面会报错。

### 3、为什么执行fn1()函数，会打印 fn1  undefined ?

```javascript
async function fn1(){
    console.log('fn1')
}
fn1()
// fn1
// Promise {<resolved>: undefined}
```
因为 async  默认会执行return 如果 return返回没有表达式或者值，那么会返回 undefined


### 4、async/await的具体使用规则
（1）凡是在前面添加了async的函数在执行后都会自动返回一个Promise对象.
（2）await必须在async函数里使用，不能单独使用.
（3）await后面需要跟Promise对象，不然就没有意义，而且await后面的Promise对象不必写then，
    因为await的作用之一就是获取后面Promise对象成功状态传递出来的参数。

```javascript
function fn() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('success')
        })
    })
}
async test() {
    let result = await fn() //因为fn会返回一个Promise对象
    console.log(result)    //这里会打出Promise成功后传递过来的'success'
}
test()
//Promise {<pending>}__proto__: Promisecatch: ƒ catch()constructor: ƒ Promise()finally: ƒ finally()then: ƒ then()Symbol(Symbol.toStringTag): "Promise"__proto__: Object[[PromiseStatus]]: "resolved"[[PromiseValue]]: undefined
// success
```

没有意义的demo （不会报错）
```javascript

async test() {
    let result = await 123
    console.log(result)
}
test()
```

### 5、async/await的错误处理方式
关于错误处理，如规则三所说，await可以直接获取到后面Promise成功状态传递的参数，
但是却捕捉不到失败状态。在这里，我们通过给包裹await的async函数添加then/catch方法来解决，
因为根据规则一，async函数本身就会返回一个Promise对象。

### 6、一个适合使用async/await的业务场景
在前端编程中，我们偶尔会遇到这样一个场景：我们需要发送多个请求，而后面请求的发送总是需要依赖上一个请求返回的数据。
对于这个问题，我们既可以用的Promise的链式调用来解决，也可以用async/await来解决，然而后者会更简洁些。

使用Promise链式调用来处理：

```javascript

function request(time) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(time)
        }, time)
    })
}

request(500).then(result => {
    return request(result + 1000)
}).then(result => {
    return request(result + 1000)
}).then(result => {
    console.log(result)
}).catch(error => {
    console.log(error)
}) 
```

使用async/await的来处理：

```javascript
function request(time) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(time)
        }, time)
    })
}

async function getResult() {
    let p1 = await request(500)
    let p2 = await request(p1 + 1000)
    let p3 = await request(p2 + 1000)
    return p3
}

getResult().then(result => {
    console.log(result)
}).catch(error => {
    console.log(error)
})
```