# vue-router
- 命名路由
- 命名视图组件
  - 如果 <router-view>设置了名称(name属性)，则会渲染对应的路由配置中 components 下的相应组件
  - router实例定义的时候传入的routes参数中的某一个route信息对应的components信息，值：vue组件 || 多个vue组件构成对象，对象属性值为router-view中对应的name值，值为vue组件
- 路由组件传参
  - 布尔模式：当routes中的某一个`route`的配置`props设置为true`，这个时候传递的`params`就会作为该路由组件的`props`
    - 命名视图，这个时候需要给对应的命名视图组件，设置{name1: true, name2: false}
  - 对象模式：给路由组件的props传递，传递静态的`route`的配置信息中的`props`设置的`props`信息
  - 函数模式：函数的参数是当前只读的`route对象`，返回值是一个对象，`属性名`是`路由组件中接收props的名称`，属性值为`route对象中的一些信息`或者`自定义的静态信息`
- 重定向和别名
  - 重定向
    - 重定向的操作也是通过routes中给route配置完成，通过配置项`redirect`，值：`path字符串` || `route对象` || 函数(参数：`to【目标路由】`,返回值：`route对象或者path字符串`)
    - 相对重定向
    ```ts
      const routes = [
          {
            // 将总是把/users/123/posts重定向到/users/123/profile。
            path: '/users/:id/posts',
            redirect: to => {
              // 该函数接收目标路由作为参数
              // 相对位置不以`/`开头
              // 或 { path: 'profile'}
              return 'profile'
            },
          },
        ]
      ```
  - 别名
    - 将 / 别名为 /home，意味着当用户访问 /home 时，URL 仍然是 /home，但会被匹配为用户正在访问 /
    - const routes = [{ path: '/', component: Homepage, alias: '/home' }]
    - alias接受的值：
      - path字符串
      - path字符串 || 相对path || 动态path字符串 数组
- 不同历史模式
  - hash模式 
    - 内部传递实际url之前添加一个`#`，这部分url不会发送服务器，不需要服务器做特殊处理
  - history模式
    - 传递的url会很正常，但是在刷新的时候，或者直接在浏览器输入框输入url的时候会出现404的错误
      - 可以通过webpack设置一下server的historyApiFallback处理，或者配置nginx，找不到的页面指向index.html
  - memory模式
    - 在node中或者ssr中使用，没有history，也不能前进/后退

## route
一个只读的对象，包含了当前路由的对象，一个会随着路由跳转响应式变化的对象

## router
路由实例对象


## 路径匹配语法
### 动态匹配
也就是路径可以动态的接受一个参数值的变化【params】【query】，如果是【params】就要在路径上添加占位符

**特殊情况：传递了两个params，只使用一个，或者每一个params，对应着一个唯一的路径：需要提供两个路径，通过动态占位符区分路由的不同**
- 仅匹配数字'/login/:redirect(\\d+)'
- `*`：零个至多个，'/login/:redirect(*)'，匹配/login, /login/one, /login/one/two, /login/one/two/three
- `+`：一个至多个，'/login/:redirect(+)'，匹配/login/one, /login/one/two, /login/one/two/three
- `?`：零个至一个, '/login/:redirect?'，匹配/login, /login/one





## 标签组件
### router-link标签
#### 参数
- exact：精确匹配(当且仅当路由匹配的时候才会匹配)，例如匹配/user/username的时候，/user的router-link也会处于激活状态，使用exact，就不会使得router-link是激活状态
- append：在当前路径跳转另外一个路径，将会拼接在当前路径后
  - ```ts
    <!-- 当前路径是 /a -->
    <router-link :to="{ path: 'b'}" append></router-link>
    <!-- 导航后的路径将是 /a/b -->
    ```
- tag：将router-link渲染成某种HTML标签
- event：定义了用来触发导航的事件
- active-class：激活状态时候的class类名，默认值是router-link-active
- exact-active-class：激活状态的时候的class类名，默认值是router-link-exact-active
- to：要导航的route信息，值：string(path字符串) || Location(route信息对象)
- replace：要导航的route信息，值：string(path字符串) || Location(route信息对象)


### router-view标签

用来渲染路径匹配到的视图组件
- name属性，如果 <router-view>设置了名称(name属性)，则会渲染对应的路由配置中 components 下的相应组件，默认值为`default`

## 行为监控

### 滚动行为

在创建router实例的时候添加`scrollBehavior`方法
- 参数(to,from,savePosition)
  - to：将要到达的路由信息
  - from：从哪个路由来的路由信息
  - savePosition：上一次上一个页面的`浏览位置的信息`【只有通过浏览器的前进/后退按钮触发】
- 返回值：滚动的位置对象
  - {x:number,y:number}
  - {selector: string(#anchor),offset?:{x:number,y:number}}：可以模仿浏览器的锚点行为

#### 异步滚动
当页面数据需要请求加载有延迟的情况下，如果页面直接滚动，会出现滚动后，数据回来，页面重新渲染，滚动失效

```js
scrollBehavior (to, from, savedPosition) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({ x: 0, y: 0 })
    }, 500)
  })
}

```
## 导航守卫
在 Vue Router 中，路由守卫的执行顺序如下：

- 全局前置守卫 (beforeEach)：当一个新的路由被触发时，全局前置守卫会首先被调用。
- 路由独享守卫 (beforeEnter)：全局前置守卫执行完毕后，会执行路由独享的守卫。
- 组件内守卫 (beforeRouteEnter, beforeRouteUpdate, beforeRouteLeave)：路由独享守卫执行完毕后，会执行组件内的守卫。
- 全局解析守卫 (beforeResolve)：组件内的守卫执行完毕后，会执行全局解析守卫。
- 全局后置守卫 (afterEach)：全局解析守卫执行完毕后，会执行全局后置守卫。
### 全局导航行为
#### 全局前置守卫
router.beforeEach(to, from) {
  return route
}
**参数**
- to
- from
- next
**返回值**
- route(用户将要去往路由信息)
- false(取消当前路由导航)
#### 全局解析守卫
router.beforeReslove(){
  
}
导航确认之前，所有组件内置守卫，被执行调用，组件或者异步组件被确认解析之后

#### 全局后置守卫
router.afterEach(to, from, failure){

}
不能取消或改变导航，也没有next参数
第三个参数为导航失败，抛出的错误
#### 路由独享守卫
router.beforeEnter(){

}
进入路由的时候触发，params/query/hash改变的时候不触发
### 组件导航行为
#### beforeRouteEnter
在渲染该组件的对应路由被验证前调用
不能获取组件实例 `this` ！
因为当守卫执行时，组件实例还没被创建！
#### beforeRouteUpdate
在当前路由改变，但是该组件被复用时调用
举例来说，对于一个带有动态参数的路径 `/users/:id`，在 `/users/1` 和 `/users/2` 之间跳转的时候，
由于会渲染同样的 `UserDetails` 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
因为在这种情况发生的时候，组件已经挂载好了，导航守卫可以访问组件实例 `this`
#### beforeRouteLeave
在导航离开渲染该组件的对应路由时调用
与 `beforeRouteUpdate` 一样，它可以访问组件实例 `this`

## 学习目的
- 页面导航：vue-router 可以帮助你在单页应用（SPA）中进行页面之间的切换，而无需重新加载整个页面例如，在一个电商网站中，可以使用路由来实现从商品列表页到商品详情页的跳转。
- 管理页面状态：vue-router 可以帮助你管理页面的历史状态，包括浏览历史、路由参数等，从而实现更加复杂的页面逻辑和交互。
- 代码分割：vue-router 可以与 webpack 等构建工具配合，实现路由级别的代码分割，按需加载不同的组件和资源，优化应用的加载性能。
- 权限控制：vue-router 提供了导航守卫，可以在路由跳转之前进行权限验证，从而实现页面级别的权限控制。例如，在一个管理后台系统中，可以通过导航守卫来验证用户是否具有访问某个页面的权限。