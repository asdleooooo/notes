# 多列布局

多列布局，用于将**内容布置到一组列框**中，就**像报纸中的列一样**

`会将内容包括所有的后代元素分段为列`

通过给一个元素添加column-count或column-width，该元素变成多列容器

## column-width

- 只支持length值和auto

用于给每列设置一个**最佳宽度**，浏览器会自动算出该宽度会在容器重分多少列，并且把额外的空间填充到这些列当中。`列宽为最小宽度，因为由于额外的空间，列可能更宽`

- 单个列可用宽度小于column-width的值的时候，`列的宽度会缩小为小于所声明的列宽`(**也就是说宽度在一列到两列之间的时候，这个宽度是随时变化的，就是宽度在0~2列宽度之间，是这个列的宽度**)

## column-count

指定显示的内容的列数

## 同事使用这两个属性

**column-count将作为最大列数**，将先按照c**olumn-width的值计算，直到达到column-count定义的列数**，在此之后，即使有足够的空间容纳指定列宽大小的列，也不会绘制

## 列间距

列之间的间距由`column-gap`属性控制，就是控制两列之间的空隙

- [`normal`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/column-gap#normal)

  ​    表示列之间的间隔宽度。在 `多列布局` 时默认间隔为 `1em`，其他类型布局默认间隔为 0。  

- [`length`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/length)

  ​    用 [`length`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/length) 来定义列之间的间隔大小。而且 [`length`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/length) 值必须是非负数的。  

- [`percentage`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/percentage)

  ​    用 [`percentage`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/percentage)（百分比）来定义列之间的间隔大小。同样的，[`percentage`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/percentage) 值也必须是非负数的。  

## 分栏线条

- column-rule-width
- column-rule-style
- column-rule-color

和border的使用方式都是一样的

## 横跨所有列

前提是没有设置每个栏元素设置width属性

- column-span:none；默认值不会横跨分栏
- column-span:all;横跨所有分栏

## 内容的平衡方式

- column-fill:balance;默认值，平衡列的内容
  - 内容在各栏之间平均分配。在分段上下文中，例如分页媒体，只有最后一个片段是平衡的。因此，在分页媒体中，只有最后一页会被平衡。
- column-fill:auto;根据列的内容调整列的高度
  - 列按顺序填充。内容仅占用其所需的空间，可能会导致某些列保持空白。

## 处理多列中的溢出

当**子项的大小大于列框**时，就会**发生溢出**。内容会溢出到下一列，而**不会被列框切割**

**解决方案**：设置`最大宽度/高度`或者`最小宽度/高度`

给大于列框的子项设置max-width：100%；

### 当多列布局的盒子装不下内容导致的溢出

解决方式是`给多列盒子设置一个最小高度`，当内容变多的时候，也会相应的变高不会发生溢出

### 当多列布局盒子高于视口的时候

这个时候用户体验不是很好，就是`要在足够高度下，才会使用多列布局，用于用户阅读`

## 多列布局内容中断

`也就是一列由于各种原因变成了分开的两列`

- **auto**

  允许但不强制在主框之后插入任何中断（page，column或region布局下）。

- **avoid**

  避免在主体框后插入任何分隔符（page，column或region布局下）。

多栏布局中的列框之间的内容中断，和分页媒体中的页面之间的中断方式相同`(就是一个屏幕中多个页面的情况)`

- break-after
  - 元素之后的分页行为
- break-before
  - 元素之前的分页行为
- break-inside
  - 元素中的分页行为