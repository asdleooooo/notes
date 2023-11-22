创建一个vite + vue的项目

```
npm create vite@latest 目录名称
```

create、init指令完全等价，https://blog.csdn.net/m0_55077449/article/details/130001956

或者通过vue-cli创建webpack项目

```
vue create 目录名称
```

![image-20240202134440281](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240202134440281.png)





-----

vue3的模板语法中可以多根标签，给自定义的组件设置class样式，样式绑定在第一个标签上

----

## ref和reactive

[变量的类型]-> [赋值 直接赋值 | 解构赋值]-> [模板语法]

- reactive只能对对象类型做响应式，ref可以对所有对象做响应式
- 对reactive的对象直接进行赋值的操作会造成响应式丢失
- reactive**对解构操作不友好**：当我们将`响应式对象的原始类型属性解构为本地变量时`，或者将该属性传递给函数时，我们将`丢失响应性连接`
- ref底层就是通过reactive实现，多嵌套了一层，在使用模板语法的时候，需要先去掉这层影响效率
- ref需要用.value调用

`Vue会将data配置项、ref对象或者reactive对象的数据变成响应式对象`，只有**代理对象是响应式的**

------

## props声明

### 没有使用<script setup/>

```js
export default {
  props: ['foo'],
  setup(props) {
    console.log(props.foo)
  }
}
```

```js
 setup(props, context) {
    // 透传 Attributes（非响应式的对象，等价于 $attrs）
    console.log(context.attrs)

    // 插槽（非响应式的对象，等价于 $slots）
    console.log(context.slots)

    // 触发事件（函数，等价于 $emit）
    console.log(context.emit)

    // 暴露公共属性（函数）
    console.log(context.expose)
  }
```

-----

## computed计算属性

- 用于`处理模板中的逻辑`，都写在模板中会变得臃肿，难以维护
- `模板中如果需要不止一次这样的逻辑`
- 返回一个ref对象

### 与方法的对比

- 计算属性只要依赖的响应式对象不发生变化，那么不会重复执行getter方法
- 方法调用总会在渲染发生时再次执行函数

-----

## 类与样式

指令:参数="值"

参数为class

- 对象 || 响应式对象
  - 通过`属性值的真假值`来确认`属性`是否存在
- 数组
- 数组嵌套三元表达式
- 对象嵌套三元表达式
- 数组嵌套对象

```
// 
<div :class="{ active: isActive }"></div>

const isActive = ref(true)



// 响应式对象
<div :class="classObject"></div>

const classObject = reactive({
  active: true,
  'text-danger': false
})
```

样式也是和上面一样，接受对象值和数组值

### 另一种响应式样式的方式

v-bind()可以在style标签中使用，script setup标签中的变量

```vue
<template>
  <div class="text">hello</div>
</template>

<script>
export default {
  data() {
    return {
      color: 'red'
    }
  }
}
</script>

<style>
.text {
  color: v-bind(color);
}
</style>
```

----------



## v-for

能接受的数据类型

- 数组，参数：(value, index) in []
- 对象，参数：(value, key, index) in {}
- 数字，参数：value in 10，value是从1开始的而不是0

**使用v-for指令的时候，需要给元素绑定一个key值，来标识元素**

--------------



## 监听事件

通过`v-on指令或者@`来监听，可以传递`$event`变量来改变event对象参数的传递位置

参数的类型：

- 内联事件处理器
- 方法事件处理器(方法名/方法的调用)

### 修饰符

#### 事件修饰符

- stop:停止事件传播，相当于event.stopPropagation
- prevent:停止默认行为，event.preventDefault
- self:仅当event.target(`触发事件的元素`)是自身的时候才会触发，event.currentTarget(`绑定事件的元素`)
- capture:表示事件会在捕获阶段触发(如果设置为true的时候)
- once:表示事件处理器只会执行一次(如果设置为true的时候)
- passive:阻止停止默认行为起作用，当这个修饰符使用的时候，事件处理器中停止默认行为失效(`当滚动行为的时候，停止默认行为和滚动的默认行为相冲突页面就不动了或者抖动`，如果设置为true的时候)

#### 按钮修饰符

- `.enter`
- `.tab`
- `.delete` (捕获“Delete”和“Backspace”两个按键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`
- `.ctrl`
- `.alt`
- `.shift`
- `.meta`:在 Mac 键盘上，meta 是 Command 键 (⌘)。在 Windows 键盘上，meta 键是 Windows 键 (⊞)。
- `.exact` 修饰符允许控制触发一个事件所需的确定组合的系统按键修饰符。(`当且仅当只按下一个键或者几个键的时候触发`)

#### 鼠标修饰符

- `.left`
- `.right`
- `.middle`

--------



## 监听器

**`默认情况下，侦听器将在组件渲染之前执行。`**

- 设置 `flush: 'post'` 将会使侦听器延迟到组件渲染之后再执行。
- 设置flush: 'sync'将会使侦听器在数据变化时执行。

可以使得每一次响应式发生变化的时候做一些有副作用的操作，状态变化就触发回调函数

`相比计算属性来说，计算属性一般不会用来做一些有副作用的操作，比如操作DOM，修改数据等`

### watch函数

1、数据源： 

- 一个ref对象
- 一个响应式对象
- 一个getter函数

2、回调函数

参数： newValue， oldValue

3、配置选项：

- **`immediate`**：在侦听器创建时立即触发回调。第一次调用时旧值是 `undefined`。
- **`deep`**：如果源是对象，强制深度遍历，以便在深层级变更时触发回调。参考[深层侦听器](https://cn.vuejs.org/guide/essentials/watchers.html#deep-watchers)。
- **`flush`**：调整回调函数的刷新时机。参考[回调的刷新时机](https://cn.vuejs.org/guide/essentials/watchers.html#callback-flush-timing)及 [`watchEffect()`](https://cn.vuejs.org/api/reactivity-core.html#watcheffect)。
- **`onTrack / onTrigger`**：调试侦听器的依赖。参考[调试侦听器](https://cn.vuejs.org/guide/extras/reactivity-in-depth.html#watcher-debugging)。
- **`once`**: 回调函数只会运行一次。侦听器将在回调函数首次运行后自动停止。 

### watchEffect函数

立即运行一个函数，同时响应式追踪其依赖，并在依赖更新时重新执行

-----

## 模板引用ref

使用模板引用的对象

- html标签，获得一个Element对象
- v-for上使用，获得一个Element对象数组
- 自定义组件上使用，获得一个Vue组件对象，对象的属性由组件defineExpose中抛出，才能使用(`Vue2中是全部暴露`)

