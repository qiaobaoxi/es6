# es6

    util1.js util2.js index.js

    util1.js
    
    export default{
    
        a:100
      
    }
    
    util2.js

    export fn1()=>{

        console.log('我是fn1');

    }
    
    export fn2()=>{
    
        console.log('我是fn2')
      
    }
    
    index.js

    import util1 from ./util1.js

    import {fn1,fn2} from ./util2.js
    
    
    
    //for

    for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。

        for (let i = 0; i < 3; i++) {
        
          let i = 'abc';
          
          console.log(i);
          
        }
        
        // abc
        
        // abc
        
        // abc
        
        上面代码正确运行，输出了 3 次abc。这表明函数内部的变量i与循环变量i不在同一个作用域，有各自单独的作用域。
        
  
  
global 对象

ES5 的顶层对象，本身也是一个问题，因为它在各种实现里面是不统一的。

浏览器里面，顶层对象是window，但 Node 和 Web Worker 没有window。

浏览器和 Web Worker 里面，self也指向顶层对象，但是 Node 没有self。

Node 里面，顶层对象是global，但其他环境都不支持。

同一段代码为了能够在各种环境，都能取到顶层对象，现在一般是使用this变量，但是有局限性。

全局环境中，this会返回顶层对象。但是，Node 模块和 ES6 模块中，this返回的是当前模块。

函数里面的this，如果函数不是作为对象的方法运行，而是单纯作为函数运行，this会指向顶层对象。但是，严格模式下，这时this会返回undefined。

不管是严格模式，还是普通模式，new Function('return this')()，总是会返回全局对象。但是，如果浏览器用了 CSP（Content Security Policy，内容安全政

策），那么eval、new Function这些方法都可能无法使用。

综上所述，很难找到一种方法，可以在所有情况下，都取到顶层对象。下面是两种勉强可以使用的方法。


// 方法一
(typeof window !== 'undefined'

   ? window
   
   : (typeof process === 'object' &&
   
      typeof require === 'function' &&
      
      typeof global === 'object')
      
     ? global
     
     : this);
     
     //json分解
     遍历 Map 结构

任何部署了 Iterator 接口的对象，都可以用for...of循环遍历。Map 结构原生支持 Iterator 接口，配合变量的解构赋值，获取键名和键值就非常方便。

const map = new Map();

map.set('first', 'hello');

map.set('second', 'world');

for (let [key, value] of map) {

  console.log(key + " is " + value);
  
}

// first is hello

// second is world
     
Array.from(document.querySelectorAll('*')); // => returns a real array.

[0, 0, 0].fill(7, 1); // => [0, 7, 7]

[1, 2, 3].findIndex(function(x) {

    return x === 2;
    
}); // => 1

['a', 'b', 'c'].entries(); // => Iterator [0: 'a'], [1: 'b'], [2: 'c']

['a', 'b', 'c'].keys();    // => Iterator 0, 1, 2

['a', 'b', 'c'].values();  // => Iterator 'a', 'b', 'c'

// Before

new Array();        // => []

new Array(4);       // => [,,,]

new Array(4, 5, 6); // => [4, 5, 6]

// After

Array.of();         // => []

Array.of(4);        // => [4]

Array.of(4, 5, 6);  // => [4, 5, 6]

首先是 from() 方法，该方法可以将一个类数组对象转换成一个真正的数组。还记得我们之前常写的 Array.prototype.slice.call(arguments) 吗？现在可以跟
  他说拜拜了~
