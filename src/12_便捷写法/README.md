
## 0. 儿子修改父亲传递的数据

父组件

```html
<template>
    <div id="app">
        <h1 v-if="show">Hello World</h1>
        <child :value="show" @input="changeShow" />
        <!-- 便捷写法 -->
        <!-- <child v-model="show" /> -->
    </div>
</template>

<script>
import Child from './views/Child';
export default {
    name: 'App',
    data() {
        return {
            show: true,
        };
    },
    components: {
        Child,
    },
    methods: {
        changeShow(value) {
            this.show = value;
        },
    },
};
</script>
```

子组件

```html
<template>
    <div>
        <button @click="handleClick">child</button>
    </div>
</template>

<script>
export default {
  name: 'Child',
  props: ['value'],
  data() {
    return {};
  },

  methods: {
    handleClick() {
      this.$emit('input', !this.value);
    },
  },
};
</script>
```

### 1. 儿子可以定制通过 v-model 传递过来默认属性

```html
<template>
    <div>
        <button @click="handleClick">child</button>
    </div>
</template>

<script>
export default {
    name: 'Child',
    model: {
        prop: 'show', // 改变传过来的默认的 value
        event: 'change', // 改变传过来的默认的 input
    },
    props: ['show'],
    data() {
        return {};
    },

    methods: {
        handleClick() {
            // this.$emit('input', !this.value);
            this.$emit('change', !this.show);
        },
    },
};
</script>
```

## 2. 关于 .sync 修饰符

父组件写法1

```html
<child :show="show" @update="changeShow($event)"/>
```

父组件写法2

```html
<child :show="show" @update="changeShow"/>
```

父组件写法3

```html
<child :show="show" @update="show=$event"/>
```

==父组件写法4==

```html
<!-- <child :show="show" @update:show="show=$event"/> -->
<child :show.sync="show"/>
```

子组件需要做对应的操作

```html
<template>
  <div>
    <button @click="handleClick">child</button>
  </div>
</template>

<script>
export default {
    name: 'Child',
    props: ['show'],
    methods: {
        handleClick() {
            // update: 是固定的
            this.$emit('update:show', !this.show)
        }
    }
}
</script>
```