# 自适应布局

默认情况下，移动浏览器会假设用户设计时所设计的宽度为 980 像素。将网页`应用980像素的宽度`，然后将所呈现的`网页缩小为屏幕实际宽度`

## viewport的meta元素

```css
<meta name="viewport" content="width=device-width" initial-scale="1">
```

width=device-width：网页宽度和手机屏幕宽度是一样的，不是980px

initial-scale:1：初始化放缩比例为1，就是不放缩

## 媒体查询

**`使用媒体查询，您可以在 CSS 中提供规则，用于描述应如何根据不同的屏幕尺寸调整此视图`**

- @media type and (feature)
  - type: all默认
  - type：print打印机
  - type：screen屏幕
  - feature
    - min-width
    - max-width

## 页面的组织方式

![image-20240304090641724](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304090641724.png)

通过媒体查询语句，对于不同的页面，产生不同的布局视图

- 宏布局：大的页面布局
- 微布局，页面中较小的组件也可以有自己的独立布局

![image-20240304091706145](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304091706145.png)

![image-20240304092021633](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304092021633.png)

![image-20240304092032324](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304092032324.png)

![image-20240304092347746](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304092347746.png)

## 排版

- 文字大小：放缩文本大小
- 放缩大小限制：clamp()
- 行长
- 行高
- 可变字体

## 自适应图片

- 固定图片：
  - 声明图片最大宽度100%
  - 基本高度自适应(保证图片比例不变)
  - object-fit:cover;
  - 设置宽高比：aspect-ratio:2/1;

- 渲染图片
  - 大小提示，给img标签设置width或者height属性，让浏览器知道图片的宽高，提前预留出位置
  - 加载提示，使用loading='lazy'，告诉浏览器是否延时加载图片
  - srcset的自适应图片![image-20240304100452659](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304100452659.png)![image-20240304100614196](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240304100614196.png)