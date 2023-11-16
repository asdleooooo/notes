# 背景样式

## 背景颜色

background-color属性定义了css中任何元素的背景颜色，接受任何有效的<color>值，**可以延伸到元素内容和内边框盒子下面**

## 背景图像

background-image属性可以在一个元素的背景中显示一个图像，**大图不会缩小适应盒子，小图则会平铺填充方框**

- 可以设置一个或者多个背景
- url值或者渐变属性值

### 控制背景的平铺行为

background-repeat属性用于控制图像的平铺行为

- no-repeat，阻止背景重复平铺
- repeat-x，仅水平方向上重复平铺
- repeat-y，仅垂直方向上重复平铺
- repeat，默认值

### 调整背景图像的大小

- 可以接受长度和百分比值
- auto，以背景图片比例放缩图片
- cover，图像会覆盖整个盒子区域
- contain，浏览器会将图像调整到合适框内，会有空隙

**如果是一个值，另外一个值默认为auto(自己根据比例自适应)，可以给多个图片背景设置size**

### 调整背景图像的位置

background-position属性允许奴选择背景图片出现在它所应用的盒子上的位置，在它所在的盒子上使用了一个**坐标系统**来控制位置，（**x轴的坐标，y轴的坐标**），可以是数值也可以是百分比或者关键字，**百分比的偏移量是相对于容器的**

提供的一些位置的关键字(**图形的一些边界放在哪,也就是后面的数值从那边开始定位【left、right】【top、bottom】不能同时出现，必须一个x轴一个y轴**)：

- top
- left
- bottom
- right
- center(**用来居中图片**)

**关键字只写一个另外一个维度默认位置在50%**

#### 偏移值的计算

- **(响应容器的尺寸 - 背景图片的尺寸) * x%**

### 渐变背景

https://cssgradient.io/

### 背景附加

背景在内容滚动时的滚动方式，由background-attachment属性控制

- scroll：使元素在背景在**页面**滚动时滚动，滚动页面内容背景则不会移动
- fixed：使元素的背景固定在视口上，这样当**页面或者元素内容**滚动时，它就不会滚动
- local：将背景固定在它所设置的元素上，**当你滚动该元素背景也随之滚动**

**scroll和local的区别在于scroll在元素区块中不随着内容的滚动而滚动，它们都随着页面的滚动而滚动背景**

### background-origin

**指定背景图片background-image属性原点的位置**，当使用background-attachment为fixed时，该属性将被忽略不起作用

- border-box，图片摆放以border区域为参考
- padding-box，背景图片的摆放以padding区域为参考
- content-box，背景图片的摆放以content区域为参考

### background-clip

设置背景的元素默认只会在padding盒子以内，通过background-clip来设置延申范围，**是对于背景的裁剪**

- border-box
- padding-box
- content-box
- text,将背景的范围只在文字上

### 简写

background：image || position/size || repeat || attachment || box || box || color 

**background-origin和background-clip的区别：在于background-origin用于设置背景图片放置的位置，background-clip用于裁剪背景图片或者背景颜色**

## 边框

- border-color
- border-style
- border-width