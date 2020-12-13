## 0. 数据劫持的基本操作

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

## 1. 只能对已存在的属性进行劫持，不存在的属性没有感知，删除属性没有感知

## 2. 在 get 和 set 里面不能直接对原对象本身进行操作，需要拷贝一份原对象（可能会有性能问题），否则会栈溢出

## 3. Vue 没有提供对数组的监听（并不是 Object.defineProperty 不支持对数组的劫持），性能问题！

```js
// Vue 要求我们下面的写法
Vue.set(obj, key, value);
this.$set(obj, key, value);
// this.$set(this.arr, 0, 'xxx');
```

## 4. 对象里面还有复杂数据类型的话，需要递归劫持里面的每一个属性（性能问题）

## 5. Proxy

Proxy 可以解决以上所有问题，注意 Proxy 监听的是整个对象，但是不能深度监听（对象里面还有复杂数据类型的话还是需要递归，但操作的是对象，而不需递归对象里面的每一个属性，性能也得到了大大的提升）

==核心一句话，换成 Proxy 主要是出于性能考虑！==
