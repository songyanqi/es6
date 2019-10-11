### this 指针问题：
this 就是一个指针，指向调用函数的对象。

1、直接函数调用，this指针指向全局环境，即Window对象。
2、对象函数调用，this指针指向调用函数的对象本身。
3、构造函数调用，this指针指向新创建的对象。

### this的绑定规则有哪些?
    默认绑定
    隐式绑定
    硬绑定
    new绑定（优先级从低到高）

### 关于 this
所有的箭头函数都没有自己的this，都指向外层作用域。
箭头函数没有它自己的this值，箭头函数内的this值继承自外围作用域。

'use strict';
// 对象在Javascript 中不是一个作用域
var obj = {
  i: 10,
  b: () => console.log(this.i, this),
  c: function() {
    console.log( this.i, this)
  }
}
obj.b(); 
// undefined,该箭头函数虽然是在obj对象中定义的，但是对象在JavaScript中并不是一个作用域，该箭头函数定义时所在的作用域是Window。
obj.c(); 
// 10, Object {...}

注：对象在JavaScript中并不是一个作用域