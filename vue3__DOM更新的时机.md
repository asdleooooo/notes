# DOM更新的时机

- 当`修改响应式的状态`时，DOM就会自动更新
- DOM更新不是同步的
- Vue会在nextTick的更新周期中缓冲所有的状态的修改(不管进行多少次的状态修改，每个组件只更新一次)



