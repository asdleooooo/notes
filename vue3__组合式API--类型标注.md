# TS搭配Vue使用

## 为ref()/reactive()标注类型

ref会根据`初始化的值`推导类型，通过泛型进行推导

如果没有初始值，推导为泛型 + undefined

不推荐使用reactive()的泛型参数，因为处理了深层次 ref 解包的返回值与泛型参数的类型不同。

```ts
interface User {
  name: string;
}

const nestedRef = ref<User>({ name: 'John' });
const reactiveObj = reactive({
  user: nestedRef
});

// 此时 reactiveObj.user 的类型可能不是 User
```

