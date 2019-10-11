### 模块
首先，Module 语法是 JavaScript 模块的标准写法，坚持使用这种写法。使用import取代require。
```Javascript
// bad
const moduleA = require('moduleA');
const func1 = moduleA.func1;
const func2 = moduleA.func2;

// good
import { func1, func2 } from 'moduleA';

```
### es6 模块化
es6的模块化通过export与import来处理:
```Javascript
//常见的导出形式：

export default obj;

export const name = "hello world";
// export { name1, name2, …, };

```
在es6中，一个文件表示一个模块，模块通过export向外暴露接口，export常用于向外导出多个变量。
```Javascript

//正确写法：
export var name = 1;
// 等价于
var name = 1;
export { name }

// 导出多个变量
var a = 1;
var b = 2;
var c = 3;
export { a, b, c }

// 导出对象
export const obj = {
    name: 'hello world'
};

// 导出函数
export function fun1() {
    console.log('hello world');
}

// 直接导出引入模块
export * from './index';

//同时 引入模块时，import导入变量名称需要与export导出的变量一一对应。
import { a, b, c } from './index';

```

### export default 
```Javascript
export default表示一个模块默认的对外接口，一个模块只能有一个export default。
export default是export的语法糖，表示导出一个default接口。

const obj = {
  name: "hello world"
};

export default obj;
// 等价于
export { obj as default }; // as表示导出别名为default的接口


//引入默认导出
import obj from './index';
// 等价于
import { default as obj } from './index';


我们有时候也会看到import * 和 export * 形式。 import
import * as obj './index';


例子: 
index.js导出obj和name变量，默认导出arr数组，在app.js中通过import * as xxx引入index.js。

// index.js
const obj = {
  name: "hello world"
};

const name = "hello world";
const arr = [1, 2, 3];
export { obj, name };
export default arr;

// app.js
import * as module from "./exp/exports";
console.log(module);
console.log(module.default);
console.log(module.name);
console.log(module.obj);
//----------------------------------------------------------------

// import 使用示例
//  --file.js--
function getJSON(url, callback) {
  let xhr = new XMLHttpRequest();
  xhr.onload = function () { 
    callback(this.responseText) 
  };
  xhr.open("GET", url, true);
  xhr.send();
}
export function getUsefulContents(url, callback) {
  getJSON(url, data => callback(JSON.parse(data)));
}
// --main.js--
import { getUsefulContents } from "file";
getUsefulContents("http://itbilu.com", data => {
  doSomethingUseful(data);
});

```

