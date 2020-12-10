## 有三种基本包装类型：Number、String、Boolean

```js
// 过程
let str = 'hello world'; // string
// 为什么 str 是一个普通数据类型却可以通过点调用 replace 方法呢？
// let newStr = str.replace(' ', '~~~');

// 上面 1 行，相当于下面 3 行，这 3 行是 JS 内部悄悄做的
let temp = new String(str); // 就是把普通数据类型 string 转换成了 包装类型 String
let newStr = temp.replace(' ', '~~~');
temp = null;

console.log(newStr);
```

## 所有对基本数据类型属性的访问都会触发那 3 步

```js
let str = 'con';
console.log(str.color); // undefined

// 有下面这样一个过程
/* let temp = new String(str);
console.log(temp.color);
temp = null; */
```

## 基本包装类型和对象最大的差异

```js
// 在于生命周期不一样，对象是离开当前作用域的时候销毁
// 基本包装类型转瞬即逝，只在当前行运行的时候有效
```