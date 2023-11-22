# 响应式对象

## 每一个对象都响应式代理

<img src="C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240219100140446.png" alt="image-20240219100140446" style="zoom: 50%;" />

<img src="C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240219100117797.png" alt="image-20240219100117797" style="zoom:50%;" />

Vue中的响应式代理是深层的代理，给每一个对象都代理了，`对于深层次的代理对象，不会调用父对象的set拦截器，但是会调用父对象的get拦截器`

- 对原始对象进行操作不会触发拦截器，对代理对象进行操作会触发拦截器
- 对`同一个原始对象`使用reactive获得的都是相同的`响应式代理对象`
- 只有**代理对象**是响应式的