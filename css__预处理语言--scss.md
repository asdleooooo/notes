# scss

一个css预处理语言

语法格式：

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;


body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

## 变量

![image-20240228102556788](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240228102556788.png)

- 普通变量
- 默认值变量，通过在值后面加!default的方式设置(`会被重新定义的变量覆盖`)

**`在选择器、函数、混合宏...的外面定义的变量为全局变量`**

## 嵌套

- 选择器嵌套
- 属性嵌套：面对css中有些前缀相同后缀不一样的情况
- 伪类嵌套：借助&配合使用

## 混合宏

**`处理大段相似的样式`**

```scss
@mixin border-radius{
    -webkit-border-radius: 5px;
    border-radius: 5px;
}

@mixin box-shadow($shadow...) {
  @if length($shadow) >= 1 {
    @include prefixer(box-shadow, $shadow);
  } @else{
    $shadow:0 0 4px rgba(0,0,0,.3);
    @include prefixer(box-shadow, $shadow);
  }
}
```

- 定义:@mixin 名称(参数:默认值){}或@mixin 名称{}
- 使用:@include 名称;

**不足：并不能智能的将相同的样式代码块合并在一起**

## 继承

- @extend来继承已存在的样式块

## 占位符

- %name表明这个样式代码块是一个模板

![image-20240228133319455](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240228133319455.png)

## 插值

- #{}，把静态的地方变成动态的，比如变量名，@include名，@extend名

## 数据类型

- 数字：1，2，10px
- 字符串：'foo' baz
- 颜色：#fff
- 布尔值：true/false
- 空值：null
- 值列表：用空格或者逗号分开

## 运算

变量或属性都可以做加法,可以进行，变量运算，数字运算，字符运算

### 加法/减法

`不同类型的单位的值相加会报错`

### 乘法/除法

两个数据都带有值，就会报错

- 相同单位
- 一个数据带单位一个不带
- 除法在使用的时候要添加括号(a/b)

## @if boolean{} @else {}

通常情况下，以下值被视为假值：

- 数字 0
- 空字符串 ""
- 空列表 ()
- `null` 和 `undefined`（在某些情况下）

其他所有值都被视为真值。

## @for循环

- @for $i from 开始 to 结束{}
- @for $i from 开始 range 结束 {}

## @while循环

只要 @while 后面的条件为 true 就会执行

## @each循环

- @each $i in <list>

## 函数

### 字符串函数

- 删除字符串中的引号:unquote()
- 添加字符串的引号:quote()
- 变大写:To-upper-case()
- 变小写:To-lower-case()

### 数字函数

- percentage($value)：将一个不带单位的书转化为百分比值
- round()：将数值四舍五入
- ceil()：将大于自己的小数转换成下一个整数
- floor()：去掉小数位部分
- abs()：返回一个属的绝对值
- min()：找出多个值的最小值
- max()：找出多个值的最大值
- random()：获取随机数

### 列表函数

- length()：返回列表长度
- nth(list, n)：返回一个列表中某个标签的值，n从1开始
- join(list1, list2)：将两个个列表连接在一起，变成一个列表
- append(list1,val)：将某个值放在列表最后
- zip(list，list，list)：将一个列表转化为多维的，每个单一的列表个数值必须是相同的
- index(list,val)：返回val所在的list中的索引

### 判断函数

- type-of()：返回一个值的类型
- unit()：返回一个值的单位
- unitless()：判断一个值是否带有单位
- comparable(number-1,number-2)：判断两个值是否可以做加减合并

### Maps的函数

- map-get(map, key)：根据给定的key值，返回map中相关的值
- map-merage(map1, map2)：将两个map合并成一个新的map
- map-remove(map, key)：从map中删除一个key，返回一个新map
- map-keys(map)：返回map中的所有key
- map-values(map)：返回map中的所有value
- map-has-keys(map, key)：判断map中是否有对应的key，返回true/false
- keywords(args)：将属性转化为map

## Map

键值对形式的类型

```scss
$theme-color: (
    default: (
        bgcolor: #fff,
        text-color: #444,
        link-color: #39f
    ),
    primary:(
        bgcolor: #000,
        text-color:#fff,
        link-color: #93f
    ),
    negative: (
        bgcolor: #f36,
        text-color: #fefefe,
        link-color: #d4e
    )
);
```

## @规则

### @import

能够导入 Sass 和 CSS 样式表，提供对 mixin、函数和变量的访问