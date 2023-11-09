# 包含块

一个元素的尺寸和位置经常受到这个元素的包含块的影响，**大部分情况下，包含快就是合格元素最近的祖先块元素的内容区域**

浏览器：展示文档的时候，**每一个元素都产生一个盒子**，这个盒子由content + padding + border + margin构成

## 如何确定一个元素的包含块？

元素的尺寸和位置，通常都会收到包含块的影响。**【width，height，padding，margin，position】**这些属性被设置为**百分比值**的时候，这些百分比的计算值都由元素包含块计算得来。

### 确定包含块

确定以恶搞元素的包含块的依据时这个元素的**position**属性

1、如果position属性为**static、relative或stick**的时候，包含块可能由**它的最近的祖先块元素的内容区边缘组成**

2、如果position属性为**absolute**，包含块由它最近的**值不是static的祖先元素**内边距区边缘组成

3、如果position属性为**fixed**，在连续媒体的情况下 (continuous media) 包含块是 [viewport](https://developer.mozilla.org/zh-CN/docs/Glossary/Viewport) 【**就是屏幕**】,在分页媒体 (paged media) 下的情况下包含块是分页区域 (page area)。

4、position属性为absolute或fixed，包含块也可能由满足一下条件的父元素内边距区域组成

- transform不是none
- 火狐filter值不是none或will-change
- contain的值时layout、paint、strict或content
- backdrop-filter值不是none

**根元素<html>所在的包含块是一个称为初始包含块的矩形，它具有视口的尺寸**