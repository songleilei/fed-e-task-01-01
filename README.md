# fed-e-task-01-01

#### ES 新特性与 JS 异步编程、TypeScript 模块作业

1. 请说出下列最终的执行结果，并解释为什么？

   ```javascript
   var a = [];
   for (var i = 0; i < 10; i++) {
     a[i] = function () {
       console.log(i);
     };
   }

   a[6](); // 输出 10
   ```

   原因：作用域有全局作用域，函数作用域，块级作用域。上题 var 定义的变量是全局作用域。

2) 请说出下列最终的执行结果，并解释为什么？

   ```javascript
   var tmp = 123;
   if (true) {
     console.log(tmp);
     let tmp = 456;
   }

   // 报错
   ```

   原因：let 不存在变量提升。下面是查阅资料的一段解释

   > 当程序的控制流程在新的作用域（`module` `function` 或 `block` 作用域）进行实例化时，在此作用域中用 let/const 声明的变量会先在作用域中被创建出来，但因此时还未进行词法绑定，所以是不能被访问的，如果访问就会抛出错误。因此，在此流程到建变量，到变量可以被访问之间的这一段时间，就称之为暂时死区。
   > [ES6 中 let 暂时性死区详解](https://segmentfault.com/a/1190000015603779) \*

3. 结合 ES6 新语法，用最简单的方式找出数组中的最小值？

   ```javascript
   var arr = [12, 34, 32, 32, 89, 4];

   console.log(Math.min(...arr));
   ```

4) 请详细说明 var，let，const 三种声明变量的方式之间的具体差别？

   ```javascript
   // var 变量声明提升
   console.log(varA); // undefined
   var varA = 123;

   // let const 声明不可提升
   let letA;
   console.log(letA); // undefined

   // const 初始化必须指定值
   const constA; // Missing initializer in const declaration
   ```

5. 请说出下列代码最终输出的结果，并解释为什么？

   ```javascript
   var a = 10;
   var obj = {
     a: 20,
     fn() {
       setTimeout(() => {
         console.log(this.a);
       }, 0);
     },
   };

   obj.fn(); // 20
   ```

   原因：obj.fn() === obj.fn.call(obj) 函数中 this 指向 obj，setTimeout 中使用**箭头函数默认绑定外层 this 的值**。

   > 箭头函数没有自己的 this, 它的 this 是继承而来; 默认指向在定义它时所处的对象(宿主对象)。[箭头函数中的 this](https://juejin.im/post/5c8f5ee5f265da612254a9ba)

6) 简述 Symbol 类型的用途？

   全局定义唯一的变量，防止重复。

7. 说说什么是浅拷贝、什么是深拷贝？

   源值：origin

   复制值：target

   如果改变 target 的值引起 origin 值的变化就是浅拷贝，反之就是深拷贝。

8) 谈谈你是如何理解 **JS** 异步编程的，**Event Loop** 是做什么的，什么是宏任务，什么是微任务？

   **JS 异步编程**：不是同步执行的，都属于异步编程。

   **Event Loop**：Event Loop 一直循环执行，将消息队列中的回调放到执行栈中执行。

   **宏任务** vs **微任务**：银行柜员给每位顾客办理业务。每位顾客的业务就属于**宏任务**，办完正事之后，推荐个理财，或者办理其他事，可以算作**微任务**。

   > [微任务、宏任务与 Event-Loop](https://juejin.im/post/5b73d7a6518825610072b42b)

9. 将下面异步代码使用 Promise 改进？

   ```javascript
   setTimeout(() => {
     var a = "hello";
     setTimeout(() => {
       var b = "lagou";
       setTimeout(() => {
         var c = "i ❤️ u";
         console.log(a + b + c);
       }, 10);
     }, 10);
   }, 10);

   Promise.resolve("hello")
     .then((a) => a + "lagou")
     .then((b) => {
       var c = "i ❤️ u";
       console.log(b + c);
     });
   ```

10) 请简述 **TypeScript** 与 **JavaScript** 之间的关系？

    TypeScript 是 JavaScript 的超集。TypeScript 编译后为 JavaScript。

    JavaScript 是 ECMAScript 的实现和扩展。

    > 引用知乎@郭凯 的一张图片
    >
    > https://pic1.zhimg.com/80/v2-c327c810e7b80cd27568e92d5a6d5721_720w.jpg

11. 请谈谈你所认为的 **TypeScript** 优缺点？

    优点：类型系统

    缺点：学习成本
