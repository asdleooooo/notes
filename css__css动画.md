# 动画

可以使用关键帧对css属性值，进行动画处理。`关键帧描述了动画元素在某个特定的事件应该如何呈现`，你可以设置`动画的持续时间`、`重复次数`、`延迟启动`等方面

## 配置动画

```
/* @keyframes duration | easing-function | delay |
iteration-count | direction | fill-mode | play-state | name */

/* @keyframes duration | easing-function | delay | name */
```

`animation`属性或其子属性：

- animation-name:指定@keyframes描述的关键帧名称

- animation-duration:设置动画周期时长

- animation-delay:设置延时

  - 单位：s/ms
  - 自然数，负值会导致动画立即开始

- animation-direction:设置动画每次运行完是反向运行还是重新回到开始位置重复运行

  - normal,正向播放
  - reverse,反向播放
  - alternate,动画在每个循环种正反交替播放
  - alternate-reverse,动画在每一个循环中正反交替播放

- animation-iteration-count：设置动画重复次数，infinite无限次重复动画

- animation-play-state:允许暂停和恢复动画

  - paused,暂停

  - running,运行

- animation-timing-function:设置动画的速度，就是简历加速曲线

  - 关键字
  - 自定义

- animation-fill-mode:指定动画执行前后如何为目标元素应用样式

  - none,回到默认值
  - forwards,保留最后一个状态

## 配置关键帧

@keyframes name {

form/0% {}

to/100% {}

}