## 0. 回答技巧

**一般情况下，一个问题都可以从这 3 个方面来回答！首先是什么？解决了什么问题？有没有什么替代方案？**

举例：说一下 Promise

> 是什么？

Promise 是一个函数/对象，一般作为构造函数来使用（说白了一般都要 new 一下 Promise）...

> 解决了什么问题？

解决了回调地狱的问题，但是 Promise 本身并不能简化代码...

> 替代方案？

所以啊，工作当中我用的最多是 async/await...

## 1. Polyfill

实现一个 reduce、filter、map、forEach、find、findIndex... some

## 2. throttle 和 debounce

防抖（debounce）和节流（throttle）都是性能优化的一种手段，debounce：重复触发（事件）不执行，不触发的一段时间后才执；throttle：重复触发（事件）也执行，只不过执行的频率变低了

## 3. 组合继承

```js
// 组合继承 = Call 式继承（继承的是属性） + 原型继承（继承的是方法）
```

```js
// Call 式继承
Person.call(this, name, age);
```

```js
// 原型继承（继承的是方法）
Star.prototype = new Person();
Star.prototype.constructor = Star;
```

## 4. JS 垃圾回收（GC => Garbage Collection）

**为什么要有垃圾回收/什么是垃圾回收**

JS 中无论声明变量、定义函数，实际上来说都需要在内存当中开辟一个空间去存储，如果说只有存储没有销毁（回收）的过程，内存肯定支撑不了，当前程序/甚至其他程序可能直接崩溃！

**JS 怎么去做垃圾回收呢**

V8 引擎会有**垃圾收集器**，会自动的进行回收，绝大多数情况下都不需要我们操心

**一般垃圾回收有哪些方式呢**

引用计数

一个对象每引用一次都会加 1，什么时候这个对象的引用变成 0 了，就会被垃圾回收器回收

```js
// 把这个对象（O）的引用给了 obj1 这个变量
var obj1 = { name: 'ifer' }; // +1
var obj2 = obj1; // 这个对象 O 又被引用了一次，+1

obj1 = null; // 这个 O 的引用少了一次，-1
obj2 = null; // 这个 O 的引用又少了一次，-1

// 此时 O 的引用还有多少次？还有 0 次，被垃圾回收器回收
```

引用计数的问题？解决不了循环引用的问题

```js
var obj1 = { name: 'ifer' }; // 这个对象 O1 +1
var obj2 = { age: 18 }; // 这个对象 O2 被引用了 1次，+1

obj1.xxx = obj2; // 这个对象 O2 又被引用了 1次，+1
obj2.xxx = obj1; // 这个对象 O1 又被引用了 1 次， +1

obj1 = null; // 这个对象 O1，-1
obj2 = null; // 这个对象 O2，-1
```

标记清除

1. 给所有的变量加上标记

2. 把所有可达的变量（可达值，通过某种方式可以被访问的变量）的标记去掉

3. 剩下的所有带标记的变量就是待删除的了（就是要被GC）

4. GC

JS 高级程序当中说的确实是删除的带标记的变量

**在写代码的时候哪些情况可能会造成内存泄露**

什么是内存泄露，这个对象没有被引用了，但是还没有被GC

1. 不小心的全局变量

```js
function fn() {
  age = 18; // 忘了加 var 了，当成的全局的去处理了
}
fn();
```

```js
function fn() {
  this.age = 18; // 也是全局的
}
fn(); // window.fn()
```

2. 尽可能的少用闭包

3. DOM 引用

```js
oDiv.addEventListener('click', function() {
  console.log(1);
});
// 从页面当中删除 oDiv
document.removeChild(oDiv);
// 即便删了
oDiv.click(); // 还是能输出 1 的

// 解决
oDiv = null;
```

...