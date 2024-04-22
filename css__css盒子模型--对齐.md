# 对齐

## 对齐的种类

- 位置对齐：通过**对齐主体**与**它对齐容器间的关系**来指定**对齐主体的位置**
- 基线对齐：这些关键字把对齐看作在**一个对齐上下文**中**多个对齐主体的基线之间的关系**
- 分布对齐：这些关键字把对齐看作多个对齐主体间空间的分布

-----

## 较老的对齐方式

- 利用text-align对齐文本
- 利用auto margin对齐块
- 利用vertical-align属性在table或者inline-block布局中对齐块【vertical-align只对**行内元素**、**行内块元素**、**表格单元格元素生效**】
- 绝对定位和相对定位对齐
- float对齐

-----

## 基线

x字母的下边缘线就是基线

‘inline-block’的基线是**正常流中最后一个line box的基线**, 除非，这个line box里面既没有line boxes或者本身’overflow’属性的计算值而不是’visible’, **这种情况下基线是margin底边缘**。

**正常流（Normal Flow）：** 正常流是 HTML 文档中元素默认的布局方式，元素按照其在 HTML 中出现的顺序一个接一个地放置。例如，下面是一个包含两个 `inline-block` 元素的简单 HTML：

```
html
```

1. ```
   <div class="example">
       <span>Inline Block 1</span>
       <span>Inline Block 2</span>
   </div>
   ```

2. **基线（Baseline）：** 元素的基线通常是其文本基线，即文本底部的水平线，用于对齐行内元素。在上述例子中，每个 `<span>` 元素都有一个基线。

3. **最后一行框（Last Line Box）：** 如果这些 `inline-block` 元素包含多行文本，那么最后一行的基线将成为元素的基线。例如，如果第一个 `<span>` 元素包含两行文本，那么第二个 `<span>` 元素将以第一个 `<span>` 元素最后一行的基线对齐。

4. **无流动中的行框或溢出不可见：** 如果 `inline-block` 元素没有包含任何行内文本（即无流动中的行框），或者它的 `overflow` 属性被设置为非 `visible` 的值，那么基线将是元素底部边缘。

示例 CSS：

```
css
.example span {
    display: inline-block;
    border: 1px solid black;
    margin: 5px;
    padding: 10px;
}
```

在这个例子中，如果两个 `inline-block` 元素都包含单行文本，它们的基线将是文本的基线。如果它们包含多行文本，那么基线将是最后一行的基线。如果其中一个元素的 `overflow` 属性被设置为非 `visible` 的值，那么基线将是该元素的底部边缘。











