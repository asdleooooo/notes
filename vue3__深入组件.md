# 组件

## 组件的注册

### 全局注册

- 通过app.component()注册全局组件，返回app实例

### 局部注册

- 在<script setup/>语法糖中只需要引入，不需要注册
- 没有使用语法糖的话，就需要通过通过components配置项进行注册

**`全局注册的组件会被打包进每一个js文件中，即使你实际上没有使用`**

## props

props遵循单项数据流，子组件无法修改父组件传入的值，props作为一个`只读属性`

- 当`props传递的值只是一个初始值`，`后续`要对这个`初始值进行修改`，就可以在`const value = ref(props.value)；`这种方式
- 当需要对props的值进行转换，可以使用computed函数
- **`特殊情况就是当props传递的值是一个对象或者数组类型的时候，子组件可以修改对象或者数组的内部属性实现修改父组件的状态的一个目的，但比较消耗性能`**

### props声明

一个组件需要声明props，用来`区分那些是props那些是attrs`

- 在<script setup/>语法糖中，使用defineProps编译宏来声明
- 在没有使用语法糖的情况下，就需要通过props配置项来进行props的声明

### props值的类型

- 字符串数组的形式,['attr']
- 对象的形式,{attr: type(预期类型)}

### 动态/静态的props

- 静态的用于一些配置项，不会动态的发生改变，对组件进行一些设置
- 动态的就是一些数据项，随着用户的操作数据会发生变化

### props使用一次绑定，绑定多个props

```js
const post = {
  id: 1,
  title: 'My Journey with Vue'
}

<BlogPost v-bind="post" />
```

等价于

```js
<BlogPost :id="post.id" :title="post.title" />
```

### props校验

props可以传递的值为数组或者对象

- type类型除了那些系统提供的以外，可以自己使用构造函数定义的类型

- 对象的话，props参数也是一个对象的话，可以设置type、default、required
  - 默认情况下，required为false，default为undefined(除了Boolean以外)
  - 除 `Boolean` 外的未传递的可选 prop 将会有一个默认值 `undefined`
  - 如果声明了 `default` 值，那么在 prop 的值被解析为 `undefined` 时，无论 prop 是未被传递还是显式指明的 `undefined`，都会改为 `default` 值

### Boolean 类型转换

为了贴近原生对于布尔类型的属性的操作

例如：<a disabled/>

Vue会将布尔类型的数值转换，如果props的属性的值为数组的话，则`只转换第一个值为布尔类型的属性`

## 组件v-model

可以在组件上实现双向绑定，用于表单输入类控件上

vue3为组件定义提供了defineModel(`3.4+`)，对model的类型，以及默认值进行限制(`以前是在props中进行接收以及限制`)

```
const count = defineModel("count", { type: Number, default: 0 })
```

```js
// 子组件：
const model = defineModel({ default: 1 })

// 父组件
const myRef = ref()

<Child v-model="myRef"></Child>
```

常见修饰符：

- trim
- number
- lazy

也可以自定义修饰符：https://cn.vuejs.org/guide/components/v-model.html

## 透传

给一个组件传递的参数中，没有被组件的props或者emits所声明或者v-on的监视器

- class
- style
- id

这些属性在使用了透传之后，就会作用在使用了透传的元素上，而不是第一个根元素上

### 禁用 Attributes 继承

```js
<script setup>
defineOptions({
  inheritAttrs: false
})
// ...setup 逻辑
</script>
```

**`可以在模板中直接使用$attrs来进行访问，也可以引入useAttrs函数，同时slots也是可以通过$slots进行访问的，不需要使用useSlots函数`**

## 插槽

由两部分构成

- 插槽内容(`父组件`)
- 插槽出口:<slot></slot>标签，标签内部设置的内容为默认内容(`子组件`)

`插槽内容只能访问，所在组件的数据，无法访问子组件的数据`

插槽的用法：

- 具名插槽
  - 父组件通过<template #name></template>
  - 子组件通过<slot name="name"></slot>

- 动态插槽名

  - 父组件<template #[name]></template>

- 作用域插槽

  - 父组件通过<template #name="绑定的参数">
  - 子组件子组件通过<slot name="name" v-bind="绑定的参数"></slot>

  ## 依赖注入

  ```js
  import { ref, provide } from 'vue'
  
  const count = ref(0)
  provide('key', count)
  
  
  import { inject } from 'vue'
  
  export default {
    setup() {
      const message = inject('message')
      return { message }
    }
  }
  ```

  