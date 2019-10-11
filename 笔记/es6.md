### 一、let const var

let：ES6 新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。
let {
   1、 不存在变量提升。
   2、 暂时性死区。
   3、 不允许重复声明。 
}

作用域 {
    全局作用域
    函数作用域
    块级作用域
}
ES6 的块级作用域允许声明函数的规则，只在使用大括号的情况下成立，如果没有使用大括号，就会报错。

ES5 规定，函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明。

const: const声明一个只读的常量。一旦声明，常量的值就不能改变。
const foo = Object.freeze({}); // 冻结对象

## 箭头函数：
### 基本用法：
ES6 允许使用“箭头”（`=>`）定义函数。

```javascript
  var f = v => v; 相当于 function f(v){ return v}

  this.s1 = 0;
  this.s2 = 0;
  // 箭头函数
  setInterval(() => this.s1++, 1000);
  // 普通函数
  setInterval(function(){
    this.s1++
  },1000)

//无传入参数，必须有()
() => { statements }

//一个传入参数，()可有可无
(singleParam) => { statements }
singleParam => { statements }

x => x * x
// 相当于
function (x) {
  return x * x;
}

//多个传入参数，必须有()
(param1, param2, …, paramN) => { statements }
(param1, param2, …, paramN) => expression

//返回一个表达式，{}可有可无，自动return表达式的值（如果是表达式，而不是执行语句）
(param1, param2, …, paramN) => expression

()=> visible = false

// equivalent to: (param1, param2, …, paramN) => { return expression; }


//返回多条语句，必须有{}
(param1, param2, …, paramN) => { statements }

//返回对象，必须使用()将{ }括起来
x => ({ foo: x })

### 关于 return

//返回一个有{}的代码块，箭头函数不会自动返回值，当需要返回一个数值的时候需要显式地使用return。
//返回一个没有{}的表达式，不需要显式地使用return，会自动return该return的值，不return而直接执行操作语句。

