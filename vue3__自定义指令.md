# 自定义指令

## 定义

- 在没有<script setup>的情况下使用directives选项进行注册，传递`自定义指令的名称`，值为`一个由指令钩子组成的对象`
- 也可以使用app.directive来定义，参数为`指令名称`，`钩子函数组成的对象`

所有的钩子函数会传递四个参数:

- el：指令绑定到的元素，可以直接操作DOM
- binding：一个对象
  - value：指令传递的值
  - oldValue：之前的值
  - arg：指令传递的参数
  - modifiers：一个包含修饰符的对象
  - instance：使用该指令的组件实例
  - dir：指令的定义对象
- vnode：绑定元素的底层VNode
- prevVnode：：代表之前的渲染中指令所绑定元素的 VNode。仅在 `beforeUpdate` 和 `updated` 钩子中可用

简化写法：

```
app.directive('color', (el, binding) => {
  // 这会在 `mounted` 和 `updated` 时都调用
  el.style.color = binding.value
})
```

**`注意：当在组件上使用自定义指令时，它会始终应用于组件的根节点，和透传 attributes 类似。需要注意的是组件可能含有多个根节点。当应用到一个多根组件时，指令将会被忽略且抛出一个警告。和 attribute 不同，指令不能通过 v-bind="$attrs" 来传递给一个不同的元素。总的来说，不推荐在组件上使用自定义指令。`**