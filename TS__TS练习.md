### Pick方法，保留类型中的某几个属性(`TS自带`)
```ts
type Pick<T extends object, K extends unknown> = {
  [Key in keyof T as Key extends K ? Key : never]: T[Key];
}
```
### Readonly方法，返回一个只读对象(`TS自带`)
```ts
type Readonly<T extends unknown> = {
  readonly [Key in keyof T]: T[Key];
} 
```
### TupletoObject方法，返回一个对象
`in操作符，遍历联合类型`，将Tuple转化为联合类型
元组转联合类型，直接使用Tuple[number]的方式
```ts
type TupletoObject<T extends keyof any[]> = {
  [Key in T[number]]: Key;
}
```
### FirstofArray方法，返回数组的第一个元素
`对于数组可以通过Array[下标]拿到某一项的属性，另外一种就是通过infer推导`
```ts
type FirstofArray<T extends unknown[]> = T extends [infer First, ...infer Rest] ? First : never;

type FirstofArray<T extends unknown[]> = T[0];
```
### GetTupleLen方法，返回元组的长度
`一定要约束为数组才能拿到这个属性`
```ts
type GetTupleLen<T extends unknown[]> = T['length'];
```
### Exclude方法，返回将一个类型中的某些类型剔除之后的类型(`TS自带`)
`联合类型是将一个或多个类型当成一个类型当作一个整体来使用`
- T extends U 比较：
  - 当我们使用 extends 关键字将联合类型 T1 | T2 | T3 与类型 U 进行比较时，实际上会对每个成员类型进行单独的比较。
  - TypeScript 会检查每个成员类型是否可以赋值给 U。
  - 如果联合类型中的任何一个成员类型可以赋值给 U，则整个联合类型会被视为可以赋值给 U。
```ts
type Exclude<T extends unknown, U extends T> = T extends U ? never : T
```
### Awaited方法，返回多层嵌套的Promise<Type>,返回这个Type

```ts
type Awaited<T extends Promise<unknown>> = T extends Promise<infer Type>
    ? Type extends Promise<unknown>
      ? Awaited<Type>
      : Type
    : never;
```
### If方法，如果传入值为true就返回第二个参数，如果传入值为false就返回第三个参数
```ts
type If<C extends boolean, T extends unknown, K extends unknown> = C extends true ? T : K;
```
### Concat方法，合并两个数组类型，合并成一个
```ts
type Concat<T extends unknown[], U extends unknown[]> = [...T, ...U];
```
### Includes方法，判断一个类型在没在另一个类型数组里
`递归遍历类型数组，然后比较类型`
```ts
import type {Equal} from './test-utils'
type Includes<T extends readonly any[], U>
= T extends [infer First, ...infer Rest]
  ? Equal<First, U> extends true
    ? true
    :Includes<Rest, U>
  : false
```
### Push方法，往数组类型中末尾添加一个类型
```ts
type Push<T extends unknown[], U extends Object> = [...T, U];
```
### UnShift方法，往数组类型中首部添加一个类型
```ts
type UnShift<T extends unknown[], U extends Object> = [U, ...T];  
```
### Parameters方法，获取函数的参数数组
```ts
type Parameters<T extends (...args: unknown[]) => any> = T extends (...args: infer P) => any ? P : never;
```