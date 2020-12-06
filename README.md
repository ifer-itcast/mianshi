## 1. Polyfill

### 实现一个 reduce、filter、map、forEach、find、findIndex... some

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