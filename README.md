## 回答技巧

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