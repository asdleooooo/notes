# 状态管理


## vuex@3
vuex单单使用单一状态树，每一个应用程序只有一个`store`实例
### state

#### 在组件中获取Vuex状态
- 通过computed计算属性来获得(`单个获取`)
  - this.$store.state.count，这样的形式来获取
- 通过mapState()函数来获取(`批量获取`)
  - 参数：
    - namespace(可选参数，string)
      - 
    - map(Array<string> | Object<string | function>)
      - ['count']
      - {count: state => state.count, countAlias: 'count'}，'count'相当于state => state.count
### getters
就是把一些state中的数据，重新组合得到的数据，每一个属性的值，都是函数，函数的参数是`state`
**使用**
- 通过属性访问(`单一获取`)
  - this.$store.getters.count
- 通过mapGetters获取(`批量获取`)
  - 参数：
    - namespace(可选参数，string)
      - 
    - map(Array<string> | Object<string | function>)
      - ['count']
      - {count: state => state.count, countAlias: 'count'}，'count'相当于state => state.count

### mutation
更改状态的唯一方法就是提交mutation
每一个mutation都有一个`事件名`和一个`回调函数`
mutation必须是同步函数(`如果是异步的，在调试工具上，很难追踪状态`)
定义：参数(`state`), 自定义传入的值(`大部分情况下应该传递一个对象`)

**使用**
在methods上定义
- `提交mutation，store.commit('mutationName', params)`(`单一提交`)
- 通过mapMutations获取(`批量提交`)
  - 参数：
    - namespace(可选参数，string)
      - 
    - map(Array<string> | Object<string | function>)
      - ['count']
      - {count: state => state.count, countAlias: 'count'}，'count'相当于state => state.count

### action
用来提交mutation，而不是直接改变状态
可以包含异步操作
定义：参数(`context`)，不是state
- context:`dispatch, commit, getters, rootGetters`
- 参数使用:参数context.commit('mutationName', params);
**使用**
- 触发action，`this.$store.dispatch('actionName', params)`(`单一触发`)
- 通过mapActions获取(`批量提交`)
  - 参数：
    - namespace(可选参数，string)
      - 
    - map(Array<string> | Object<string | function>)
      - ['count']
      - {count: state => state.count, countAlias: 'count'}，'count'相当于state => state.count
### module
可以将vuex分割成不同的模块，在一个store下的state的不同模块下
每个模块都有着，state、getters、mutations、actions
`模块内部的actions、mutations、getters在全局命名空间中`
 namespaced: true,这样设置之后，上面这些属性就在了module下的命名空间中，使用要在`getters['account/isAdmin']`、`dispatch('account/login')`、`commit('account/login')`

## pinia




## 注意
Vuex 和 Pinia 都是 Vue.js 的状态管理库，它们的主要功能是帮助开发者管理和共享 Vue 应用程序中的状态。

**Vuex 的主要功能和使用场景包括：**

- 管理和共享 Vue 应用程序中的状态，使得状态的变化更可追踪、更易于管理。
- 适用于大型单页应用程序，可以帮助你更好地组织和管理应用程序的状态，从而使代码更加清晰和易于维护。
- 解决了多个视图依赖同一状态，以及多个组件共享状态时，单向数据流的简洁性很容易被破坏的问题。
- 
**Pinia 的主要功能和使用场景包括：**

- 提供了一种简单、可靠和可扩展的方法来管理应用程序状态。
- 适用于大型单页应用程序，可以帮助你更好地组织和管理应用程序的状态，从而使代码更加清晰和易于维护。
- Pinia 通过设计提供扁平结构，就是说每个 store 都是互相独立的，谁也不属于谁，也就是扁平化了，更好的代码分割且没有命名空间。