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

## 5. Vue 中的 watch 和 computed 差异

## 6. 了解原型链污染及解决

## 7. 关于基本包装类型

## 8. 为什么 Vue3 数据的响应为什么改成了 Proxy

数据劫持的基本操作

```js
const obj = {
    name: 'ifer',
    age: 18
};
const copyObj = { ...obj };
Object.keys(obj).forEach(item => {
    Object.defineProperty(obj, item, {
        get() {
            return copyObj[item];
        },
        set(newValue) {
            copyObj[item] = newValue;
        }
    });
});
```

1. 只能对已存在的属性进行劫持，不存在的属性没有感知，删除属性没有感知

2. 在 get 和 set 里面不能直接对原对象本身进行操作，需要拷贝一份原对象（可能会有性能问题），否则会栈溢出

3. Vue 没有提供对数组的监听（并不是 Object.defineProperty 不支持对数组的劫持），性能问题！

```js
// Vue 要求我们下面的写法
Vue.set(obj, key, value);
this.$set(obj, key, value);
// this.$set(this.arr, 0, 'xxx');
```

4. 对象里面还有复杂数据类型的话，需要递归劫持里面的每一个属性（性能问题）

Proxy 可以解决以上所有问题，注意 Proxy 监听的是整个对象，但是不能深度监听（对象里面还有复杂数据类型的话还是需要递归，但操作的是对象，而不需递归对象里面的每一个属性，性能也得到了大大的提升）

==核心一句话，换成 Proxy 主要是出于性能考虑！==
