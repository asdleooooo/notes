# TS

TS = JS + 类型系统

- 提前发现错误
- 提示作用，告诉开发者函数怎么用

**`TS就是编译生成js，目标是类型校验`**

## 类型声明

- 冒号 + 类型

```ts
function toString(num:number):string {
  return String(num);
}
```

**`ts规定变量只有赋值之后才能使用，否则就会报错`**

## 类型推断

- TS会自己推断类型
- 类型推断不能保证推断出正确的类型

## any类型、unknown类型、never类型

### any类型

- 表示(变量)没有任何限制(可以被赋予任何类型)，`TS不会校验该类型，语句正确就不会报错`
- 开发者没有指定类型，类型推断无法推断出类型，TS就会认为该变量类型为any

**`把一个any赋值给其他变量，则其他变量不会再被TS校验类型`**

### unknown类型

为了解决any，污染其他变量的问题

- 表示不确定类型
- 可以接受任意类型的赋值，但是不能将值分配除unknown以外的类型

- 只能进行比较运算符、取反运算、typeof运算符、instanceof运算符、||、&&、？，其他运算符都报错

如果要使用unknown类型，就要缩小类型范围

```ts
let s: unknown = 'hello';

if(typeof s === 'string') {
  s.length;
}
```

### never类型

空类型，不可能有这样的类型(主要用于某一些类型运算之中)

## 类型系统

### 基础类型

TS继承了JS的类型设计，有八种基本类型

- boolean
- string
- number
- bigint
- symbol
- object
- undefined
- null

#### undefined和null的特殊性

**`其中undefined和null既是值也是类型`**

- 如果没有声明变量类型，赋值为undefined或者null就会被推断为any，为了避免这种情况需要开启strictNullChecks
- `任何类型的变量都可以赋值为undefined和null，并不是因为undefined和null包含在其他类型里面，是为了和JS的行为保持一致`
- 打开`--strictNullChecks`以后就不能给其他变量赋值成undefined或者null了

#### Object类型和object类型

- Object代表广义对象，所有可以转成对象的值都是Object类型的(原始值类型 + object类型 - undefined - null)
- object代表狭义对象，只包含对象、数组和函数，不包括原始值
- `注意的是Object和object类型只能包含JavaScript内置原生的属性和方法`

#### 字面量和包装对象类型

```ts
const s = new String('hello');
typeof s // 'object'
s.charAt(1) // 'e'

```

**`使用包装对象创建的string、number、boolean类型都会变成object类型`**

- Boolean 和 boolean
- String 和 string
- Number 和 number
- BigInt 和 bigint
- Symbol 和 symbol

**`使用字面量赋值大写声明类型的时候会报错，要使用小写`**

### 值类型

TS中单个值也是一种类型，值类型

- const没有设置类型，普通类型会推断为值类型，对象类型不会推断为值类型
  - ![image-20240305110355441](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240305110355441.png)![image-20240305110408765](C:%5CUsers%5CYANGY%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20240305110408765.png)因为对象里面的属性值是可变的

### 联合类型

多个类型组合成一个新类型，通过|

### 交叉类型

同时需要具有多种类型，通过&

### type命令

定义一个类型的别名，别名支持使用表达式插值语法

### typeof运算符

- TS中返回变量的TS类型，typeof参数只能是标识符
- JS中返回变量的JS类型

### 块级类型声明

在块中的作用域

## 数组类型

JS的数组在TS中分成两种类型：

- 数组
  - 类型[]
  - Array<类型>
- 元组

TS允许方括号读取数组的类型

```ts
type Names = string[];
type Name = Names[0]; // string
```

### 数组的类型推断

- 没有初始化的空数组，会被推断为any[]，后续对该数组操作，会自动更新新的类型推断
- 如果初始化为一种类型，则后续操作不是这种类型会报错

### 只读数组&const断言

- 在数组类型前面加上readonly关键字，readonly number[]是number[]的父类型
- const arr = [0, 1] as const;通过const断言创建只读数组

## 元组类型

- 表示每个成员类型可以自由设置的数组
- 为元组成员加?代表，这个元组成员是可选的,所有可选成员必须在必选成员之后
  - let a:[number,number?] = [1];
- 元组一般是一个有限长度的，也可以通过扩展运算符来表示一个不限制长度的元组[number, ...number[], number]
- `只读元组和只读数组的定义的方式一样`
- 元组的长度一旦确定之后，推断元组长度则无意义

```ts
const arr = [1, 2];

function add(x:number, y:number){
  // ...
}

add(...arr) // 报错

```

换成元组之后就不报错了

## 函数

**函数可以声明类型的地方：**

- 参数的类型：不声明类型会被推断为any类型
- 返回值的类型：void表示函数没有返回值

**一个变量被赋值一个函数：**

- const hello = function(txt: string) {console.log('hello' + txt);}
- const hello: (txt: string) => void = fcuntion(txt) {console.log('hello' + txt);}
- {(参数列表): 返回值}

**`Function表示任意函数，参数和返回值都是any类型`**

### 参数

- 可选参数，多个参数放在必选参数之后用?表示可选

- 参数解构

  - ```ts
    function sum(
      { a, b, c }: {
         a: number;
         b: number;
         c: number
      }
    ) {
      console.log(a + b + c);
    }
    ```

- rest参数
  
  - 表示所有剩余的参数，可以设置类型为数组或者元组
- 只读参数，类型前加readonly

### 函数重载

参数：不同类型或者不同个数

返回值：不同类型或者个数

函数的实现的参数要包含参数和返回值，在实现里面要做类型的限制

### 构造函数

构造函数的类型:

- new () => Animal
- {new (s: string): Animal}

## 对象类型

- 属性
  - 属性值
    - 可选，属性名后加?
    - 只读，属性名前加readonly
  - 属性名
    - 索引类型
      - {[name: string]: string}
  - 操作
    - 解构赋值

对象类型之间的父子类型，属性多的为子类型，父子类型之间可以相互等于，赋值就不行

- `子类型比父类型更加具体`
- 通常情况下遵循协变(子类型可以赋值给父类)，两个函数的变量进行赋值的时候，参数遵循逆变

`空对象，会被推断为类型为空对象的字面量`

## interface接口

为对象的模板，和对象的用法差不多

### interface的继承

- interface继承interface
  - 多个接口合并，使用extends接口列表，以逗号风格，有相同的属性不同的类型会报错
- interface继承type
  - 合并类型，生成新类型
- interface继承class
  - 继承了类但是类中有私有属性的话，声明的时候，实现不了这个接口

### 接口的合并

- 一个接口重新定义，会接口合并

  - ```ts
    interface Document {
      createElement(tagName: any): Element;
    }
    interface Document {
      createElement(tagName: "div"): HTMLDivElement;
      createElement(tagName: "span"): HTMLSpanElement;
    }
    interface Document {
      createElement(tagName: string): HTMLElement;
      createElement(tagName: "canvas"): HTMLCanvasElement;
    }
    
    // 等同于
    interface Document {
      createElement(tagName: "canvas"): HTMLCanvasElement;
      createElement(tagName: "div"): HTMLDivElement;
      createElement(tagName: "span"): HTMLSpanElement;
      createElement(tagName: string): HTMLElement;
      createElement(tagName: any): Element;
    }
    ```

### type和interface的异同

- type技能表示非对象也能表示对象，interface只能用于描述对象类型
- interface可以继承其他类型，type不能继承其他类型
- type不能多次定义
- this关键字只能在interface中使用

## class类型

- 属性的类型
- readonly修饰符
- 存取器
- 索引属性
- 类的interface接口 ，class要实现(implements)

`如果一个类和接口同名，那么接口将被合并进类`

- public
- private：子类和实例都无法使用
- protected：子类内部可以使用，实例无法使用

## 泛型

类型参数，使用泛型就要定义类型参数先

- 函数泛型
  - 在函数名后<T>，就可以在函数中使用泛型了，函数调用的时候传入泛型参数

- 接口泛型
  - 在接口名后<T>，这样声明泛型，就能使用了
  - 也可以在接口定义的方法名前使用泛型，这样就可以该函数使用的泛型其他函数用不了
- 类的泛型写法
  - 和接口的泛型写法类似
- 类型的泛型写法
  - 和上面的类似

`泛型也有默认值，一般默认值是any，可以通过=来设置，可以通过extends来限制泛型的类型`

## Enum类型

常量存放的一个容器

- 成员不赋值依次递增，赋数字类型的值依次递增
- const enum 创建enum类型编译后，使用enum的地方会换成对应的值
- enum成员不能重新赋值只读
- 同名enum合并，但是都没有设置初始值的话就会报错
- enum的成员值可以是字符串
- enum存在反向映射(`只发生在数字值的enum上，字符类型不存在`)

## 类型断言

开发者告诉TS这个变量是什么类型的

- value as Type
- <Type>value

类型断言使用的条件是`断言值和被断言值之间有一点父子类型关系`

### as const断言

断言一个值是一个常量

### 非空断言

对于一些可能为空的变量(可能为undefined或null)

- 在变量名后面添加！

### 断言函数

```ts
function isString(value:unknown):asserts value is string {
  if (typeof value !== 'string')
    throw new Error('Not a string');
}
```

## 模块

TS的模块和JS的模块的区别在于，能够允许输入输出类型

## 装饰器

装饰器的作用在于替换代码或者添加代码

### 语法：

- 定义：定义一个函数，函数的参数为value和context

- 使用：@函数名

### 装饰器

- 类的装饰器
  - value就是class类，context就是当前类的上下文对象
- 方法装饰器
- 函数装饰器
- 属性装饰器

## 运算符

### keyof运算符

用于描述对象的key和对象之间的关系

- 接受`对象类型`作为参数，返回`对象所有键名`组成的联合类型
- keyof any获得的类型是string | number | symbol
- keyof object，object本身没有属性也没有键名，返回never

### in运算符

- 在JS中判断对象是否包含属性
- TS中用来取出(遍历)联合类型的每一个成员类型

```ts
type U = 'a'|'b'|'c';

type Foo = {
  [Prop in U]: number;
};
// 等同于
type Foo = {
  a: number,
  b: number,
  c: number
};
```

### 方括号运算符

取出对象(object\数组\字符串\函数)的简直类型

```ts
type Person = {
  age: number;
  name: string;
  alive: boolean;
};

// number|string
type T = Person['age'|'name'];

// number|string|boolean
type A = Person[keyof Person];
```

### extends...?:

TS提供的类似于三元运算符

判断一个类型是否能赋值给另外一个类型，就是一个类型是否为另一个类型的子类型

### infer关键字

通常和条件运算符一起使用，在extends关键字之后的父类型之中，表示类型是推断出来的，不是外部传入，推导泛型的类型

```ts
type Flatten<Type> =
  Type extends Array<infer Item> ? Item : Type;
    
// string
type Str = Flatten<string[]>;

// number
type Num = Flatten<number>;
```

### is运算符

描述返回值是属于true还是false

### 模板字符串

可以使用模板字符串构建类型

模板字符串可以引用的类型一共6种，分别是 string、number、bigint、boolean、null、undefined。引用这6种以外的类型会报错

## 用法

-------

### 模式匹配提取

如果我们想提取类型中的某一个部分的类型

```ts
type GetValueType<P> = P extends Promise<infer Value> ? Value : never;
```
#### 数组类型
**提取第一个元素的类型**
```ts
type arr = [1,2,3];

type GetFirst<Arr extends unknown[]> = Arr extends [infer First, ...unkown[]] ? First : never;
```
**去掉数组类型的最后一个类型**
```ts
type arr = [1,2,3];
type PopArr<Arr extends unknown[]> = Arr extends [...infer Rest, unknown] ? Rest : never;

```
**去掉数组类型的第一个类型**
```ts
type arr = [1,2,3];
type ShiftArr<Arr extends unknown[]> = Arr extends [unknown, ...infer Rest] ? Rest : never;
```
#### 字符串类型
利用模板字符串进行字符串字面量类型的模糊的一个描述

**判断字符串是都以某个前缀开头**
```ts
type StartWith<Str extends string, Prefix extends string> = Str extends `${Prefix}${string}` ? true : false;
```
**利用模板字符串和infer替换一个字符串字面量类型**
```ts
type ReplaceStr<Str extends string, From extends string, To extends string> = Str extends `${infer Prefix}${from}${Suffix}` ? `${infer Prefix}${To}${Suffix}` : Str;
```
#### 函数
**在函数中提取参数、返回值的类型**
```ts
type GetParameters<Func extends Function> = Func extends (...args: infer Args) => unknown ? Args : never;
```
```ts
type GetReturnType<Func extends Function> = Func extends (...args: any[]) => infer ReturnType ? ReturnType : never;
```
用类型描述 + infer来描述你想要从一个类型中得到的类型,返回这个推导出来的类型

### 对类型做修改
type叫做类型的别名,就是声明一个变量存储类型
**重新构造做变换**
#### 数组类型的重新构造
首先有一个元组
```ts
type tuple = [1,2,3];
```
往这个元组后面添加一些新的类型
```ts
type Push<Arr extends unknown[], Ele> = [...Arr, Ele];
```
往这个元组前面添加一个新的类型
```ts
type UnShiift<Arr extends unknown[], Ele> = [Ele, ...Arr];
```
重组两个元组
```ts
type tuple = [1,2];
type tuple = ['guang', 'dong'];

type Zip<One extends [unknown, unknown], Other extends [unknown, unknown]> = One extends [infer OneFirst, infer OneSecond] ? Other extends [infer OtherFirst, infer OtherSecond]? [[OneFirst, OtherFirst], [OneSecond, OtherSecond]] : [] :[]
```
#### 字符串重新构造
使用递归 + 描述字符串类型，实现重新构造字符串类型
```ts
type DropSubStr<Str extends string, SubStr extends string> = Str extends `${infer Prefix}${SubStr}${infer Suffix}` ? DropSubStr<`${Prefix}${Suffix}`, SubStr> : Str;
```
#### 函数类型重新构造
```ts
type AppendArgument<Func extends Function, Arg> = Func extends (...arg: infer Args) => infer ReturnType ? (...args:[...Args, Arg]) => ReturnType : never;
```
#### 索引类型的重新构造
```ts
type obj = {
  name: string;
  age: number;
  gender: boolean;
}

type Mapping<Obj extends object> = {
  [Key in keyof Object]: Obj[key]
}

type ToMutable<T> = {
    -readonly [Key in keyof T]: T[Key]
}

type ToRequired<T> = {
    [Key in keyof T]-?: T[Key]
}

type FilterByValueType<Obj extends Record<string, any>, ValueType> = [Key in keyof Obj as Obj[key] extends VlaueType ? key : never] : Obj[key];
```
#### 递归复用做循环
通过函数不断调用自身解决一个个小问题，直到满足结束条件，完成这个问题的求解
**提取不确定层数的Promise中的value类型**
```ts
type DeepPromiseValueType<PromiseType extends Promise<unknown>> = 
      PromiseType extends Promise<infer ValueType> ? 
        ValueType extends Promise<unknown> ? DeepPromiseValueType<ValueType>
          : PromiseType
        : never;
```
**数组类型的递归**

反转数组
```ts
type ReverseArr<Arr extends unknown[]> = Arr extends [infer First, ...infer Rest] ? [...ReverseArr<Rest>, first] : Arr;
```
如果Arr能够被分解，那就继续分解重组为数组，如果Arr不能被分解，就返回Arr

判断数组是否存在3
```ts
type Includes<Arr extends unknown[], FindItem> = 
  Arr extends [infer First, ...infer Rest]
    ? IsEqual<First, FindItem> extends true
      ? true
      : Includes<Rest, FindItem>
    : false
```

删除一个数组项
```ts
type RemoveItem<
  Arr extends unknown[],
  Item,
  Result extends unknown[] = []
  > = Arr extends [infer First, ...infer Rest] 
    ? IsEqual<First, Item> extends true
      ? RemoveItem<Rest, Item, Result>
      : RemoveItem<Rest, Item, [...Result, First]>
    : Result;
```

构造一个数组类型，传入数组的长度和数组的元素类型
```ts
BuildArray<
  Length extends number,
  Ele = unknown,
  Arr extends unknown[] = []
> = Arr['length'] extends Length
    ? Arr
    : BuildArray<Length, Ele, [...Arr, Ele]>;
```

字符类型做递归
对于多个一样的字符替换的处理

```ts
type ReplaceStrAll<
  Str extends string,
  From extends string,
  To extends string
> = Str extends `${infer Prefix}${From}${infer Suffix}`
      ? `${Prefix}${To}${ReplaceStrAll<Suffix, From, To>}` : Str
```





-----------------
