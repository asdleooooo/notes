# 流程控制与错误处理

## 语句块

最基本的语句是`用于组合语句`的语句块。该块由`一对大括号`界定

```js
{
  ststatement_1;
  ststatement_2;
}
```

**在ES6标准之前，js没有块作用域。在一个块中引入的变量的作用域是包含函数或脚本，并且设置他们的效果会延续到块之外。也就是块语句不定义范围**

## 条件判断语句

JavaScript 支持两种条件判断语句：`if...else`和`switch`

### 错误的值

- false
- undefined
- null
- 0
- NaN
- 空字符串""

### switch语句

允许一个程序求一个表达式的值并且尝试去匹配表达式的值到一个case标签

```js
switch (expression) {
   case label_1:
      statements_1
      [break;]
   case label_2:
      statements_2
      [break;]
   ...
   default:
      statements_def
      [break;]
}

```

`可选的 break` 语句与每个 `case` 语句相关联，保证在匹配的语句被执行后程序可以跳出 `switch` 并且继续执行 `switch` 后面的语句。如果 break 被忽略，则程序将继续执行 switch 语句中的下一条语句。

## 异常处理语句

throw 抛出一个异常

try...catch...finally catch用于监听try语句的错误，finally无论是否有异常都会执行