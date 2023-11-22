# 弹性盒子

弹性盒子是一种按照**行列布局**元素的一维布局方法

- 行列布局，一维布局方式
- 元素可以膨胀填充空间
- 元素可以缩小适应空间

## flex模型说明

![image-20231122161132291](https://raw.githubusercontent.com/asdleooooo/cloudimg/master/img/image-20231122161132291.png)

**主轴**：是沿着flex**元素放置方向上延申的轴**(行或者列都行)，改轴的开始或者结束称为main start和main end

**交叉轴**：**垂直于flex元素放置方向的轴**，该轴开始和结束称为cross start和cross end

## flex-direction

设置弹性盒子主轴的方向，默认是row

- row
- row-reverse
- column
- column-reverse

## flex-wrap

flex元素单行显示还是多行显示

- nowrap
- wrap
- wrap-reverse

## flex-flow

是flex-direction和flex-wrap的一个符合属性

```css
flex-flow: row wrap;
```

## flex-shrink

**作用在contentbox上的**

指定flex元素的收缩规则，flex元素在默认宽度之和大于容器的时候会发生收缩

**负数无效，default为1**，就是收缩比例占1

## flex-grow

**作用在contentbox上的**

指定flex元素的增长比例，增长比例默认为0，负值无效，会直接忽略宽度

## flex-basis

**作用在contentbox上的**

定义了分配剩余空间之前元素的默认大小，默认值是auto，这个时候width属性会生效

**最大最小尺寸限制 > 弹性增长或收缩 > 基础尺寸**

min-width || max-width > flex-basis > width > content size

## flex

flex-grow | flex-shrink | flex-basis

单个值，两个值，三个值，对应上面的设置

## 水平和垂直对齐

### 交叉轴

#### align-items

**将所有子元素作为一个组**，控制子**元素在交叉轴上的对齐方式**，在网格布局中控制子元素在网格区域内块向轴上对称

- stretch
- center
- start
- end

#### align-self

会对齐当前网格或者弹性行中的元素，单个的元素

### 主轴

#### justify-content

弹性容器的主轴和网格容器的行向轴，分配元素周围的空间

- start
- center
- space-between
- space-around
- space-evenly

#### justify-items

- stretch
- center
- start
- end

## 顺序

order默认值为0