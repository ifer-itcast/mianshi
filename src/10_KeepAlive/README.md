## 是什么

做性能优化的，可以用来缓存组件，缓存后组件的生命周期不会被触发（当然第一次肯定会触发 created）

## 怎么用

```js
<keep-alive>
    <router-view/>
</keep-alive>
```

## 对应的钩子

有的时候确实需要在缓存的组件中做一些处理，例如请求一些接口，这个时候在哪里操作呢？

```js
activated() {
    // 可以这里操作
    console.log('激活');
},
deactivated() {
    console.log('失活');
},
```

## 是否需要缓存的 3 种方法

1、第一种

include 可以指定哪些需要被缓存

```js
<!-- 只有包含的 About 才会缓存，About 是路由配置时候的 name -->
<keep-alive :include="['About']">
  <router-view/>
</keep-alive>
```

2、第二种

exclude 可以指定哪些不需要被缓存，也可以配合 include 一起使用

```js
<keep-alive :exclude="['Home', 'News']">
  <router-view/>
</keep-alive>
```

3、第三种

路由配置表里面通过 meta 指定数据，用来判断是否需要缓存此路由

```js
const routes = [
  {
    path: '/news',
    name: 'News',
    component: News,
    meta: {
      isAlive: true // true 代表需要缓存
    }
  }
]
```

在路由出口里面做判断

```js
<keep-alive>
  <router-view v-if="$route.meta.isAlive"/>
</keep-alive>

<router-view v-if="!$route.meta.isAlive"/>
```