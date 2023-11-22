# 网格布局

## 定义

### grid

通过css属性display:grid可以定义一个css网格，可以使用grid-template-rows和grid-template-columns属性定义网格列属性和行属性

**这些属性定义的网格被称为显式网格**

如果开发者将内容防止在现实网格之外，或者以来自动布局的话，网格将需要创建额外的row或者column、tracks来包含现实网格以外的内容，**为了将在隐式网格中创建额外的轨道，来显示显式网格之外的内容**

### grid lines

使用grid布局在**显式网格**中定义轨道的同时会创建**网格线**

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 100px;
}
```

这样就会创建**三条行线和四条列线**

#### 按照网格线编号将项目放置到网格上

```css
.item {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 3;
}
```

#### 命名网格线

在显式网格创建的网格线可以被命名，**在轨道大小信息之间或者之后的方括号中命名**。当放置1一个项目时，你可以**使用这些名词代替编号**

```CSS
.wrapper {
  display: grid;
  grid-template-columns: [col1-start] 1fr [col2-start] 1fr [col3-start] 1fr [cols-end];
  grid-template-rows: [row1-start] 100px [row2-start] 100px [rows-end];
}
.item {
  grid-column-start: col1-start;
  grid-column-end: col3-start;
  grid-row-start: row1-start;
  grid-row-end: rows-end;
}

```

### grid tracks

网格轨道，**是两条网格线之间的空间**。它们通过使用属性grid-template-columns和grid-template-rows活着简写属性grid和grid=-template在显式网格中定义。网格轨道也可以在隐式网格中创建，**通过将一个网格项目定位到显式网格中创建的轨道外面**

#### 显式网格中的轨道大小

当使用 [`grid-template-columns`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-template-columns) 和 [`grid-template-rows`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-template-rows) 定义网格轨道

#### 隐式网格中的轨道大小

隐式网格中创建的轨道**默认为自动大小**，但可以通过 [`grid-auto-rows`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-auto-rows) 和 [`grid-auto-columns`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-auto-columns) 属性来定义这些轨道的大小。

![image-20231204091523775](https://raw.githubusercontent.com/asdleooooo/cloudimg/master/img/image-20231204091523775.png)

紫色的这个在隐式网格中轨道为自动高度，随着item告诉的变化而变化

### grid cell

在id布局中，**网络单元格是css网格中的最小单元**。它是**四条网格线之间的空间**

### grid areas

**网格区域**是网格中**由一个或者多个网格单元格组成的矩形区域**

一定是矩形，不能是别的形状

在下面的例子中，有一个网格容器包含两个网格项目，我用 [`grid-area`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-area) 属性命名它们，然后用 [`grid-template-areas`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-template-areas) 把它们放在网格上。这将创建两个网格区域，一个覆盖四个网格单元格，另外一个覆盖两个。

```css
.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 100px;
  grid-template-areas:
    "a a b"
    "a a b";
}
.item1 {
  grid-area: a;
}
.item2 {
  grid-area: b;
}

```

### gutters

网格间距是网格轨道之间的间距

**能够导致轨道被间隔开来的，除了网格间距属性，还有margins，padding或者使用盒模型对齐中的空间分布属性**

### 网格轴

css网格布局是一种二维布局方法，能够按行和列对内容布局。在任何网格布局中都有两个轴列轴和行轴

沿着这些轴可以使用和对齐规范中定义的属性，对元素按照块向轴或者行向轴对齐

#### 对齐元素到块轴

align-self和align-items用于控制元素在**块方向的轴上对齐**，通过这两个属性，把元素的对齐方式设置为以下的值：

- `auto`

- `normal`对于那些 flex 元素而言，行为与 `stretch` 类似。

  对于那些 grid 元素而言，行为与 `stretch` 类似，但对于具有长宽比或固有尺寸的盒子，其行为与 `start` 类似

- `start`将元素与容器的主轴起点或交叉轴起点对齐。

- `flex-start`只在 flex 布局中使用，将元素与 flex 容器的主轴起点或交叉轴起点对齐。

- `flex-end`只在 flex 布局中使用，将元素与 flex 容器的主轴末端或交叉轴末端对齐。

- `end`将元素与容器的主轴末端或交叉轴末端对齐。

- `center`flex 元素的外边距框在交叉轴上居中对齐。如果元素的交叉轴尺寸大于 flex 容器，它将在两个方向上等距溢出。

- `stretch`如果（多个）元素的组合大小小于容器的大小，**其中自动调整大小的元素将等量增大，以填满容器**，同时这些元素仍然保持其宽高比例的约束。

- `baseline`

- `first baseline`

- `last baseline`所有 flex 元素都对齐，以使它们的 [flex 容器基线](https://drafts.csswg.org/css-flexbox-1/#flex-baselines) 对齐。距离其交叉轴起点和基线之间最远的元素与行的交叉轴起点对齐。

#### 对齐元素到行轴

justify-items和justify-self用于对齐元素到行轴，可选值和align-self一样

### grid item的大小由什么决定

在 CSS Grid 布局中，Grid项（grid item）的大小由以下几个因素共同决定：

1. **`grid-template-rows` 和 `grid-auto-rows`：** 这两个属性用于定义行的大小。`grid-template-rows` 用于显式定义特定行的大小，而 `grid-auto-rows` 用于定义未在 `grid-template-rows` 中明确指定大小的自动行的大小。

   ```
   css
   ```

```
.wrapper {
  display: grid;
  grid-template-rows: 100px 1fr; /* 显式定义前两行的大小 */
  grid-auto-rows: 50px; /* 自动行的默认大小 */
}
```

**`height` 属性：** 如果你为 Grid 项元素明确设置了 `height` 属性，那么它将覆盖任何通过行的定义或自动行高度设置的值。

```
css
.item1 {
  height: 150px; /* 显式设置 Grid 项的高度为150像素 */
}
```

**`align-self` 和 `align-items` 属性：** 这两个属性用于控制 Grid 项在交叉轴（垂直轴）上的对齐方式。`align-self` 用于单个项，而 `align-items` 用于整个容器。它们可以影响 Grid 项的高度，特别是在没有明确设置高度时。

1. ```
   .item1 {
     align-self: stretch; /* 在交叉轴上拉伸以填充整个高度 */
   }
   
   .wrapper {
     align-items: start; /* 整个容器的 Grid 项在交叉轴上顶部对齐 */
   }
   ```

这些因素一起协同工作，决定了 Grid 项的最终大小。在实际应用中，根据布局需求，你可以使用这些属性来灵活地调整 Grid 项的尺寸和对齐方式。

### 与弹性盒子相比较

justify-self和justify-items在弹性盒子中未被实现，这是因为言行盒子的本质是一维的。在轴上会有很多元素，无法单独对齐某一个元素。

**要在弹性布局中实现眼主轴上对齐元素，可以使用justify-content属性**

[`place-items`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/place-items) 属性是对 [`align-items`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/align-items) 和 [`justify-items`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-items) 的简写。