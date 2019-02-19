---
title: typescript类型
date: 2018-12-17 21:33:27
tags:
  - typescript
categories: 
  - 前端
---
布尔、字符串、数字、数组、对象
在原生数组的基础上
##元组 Tuple
元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 比如，你可以定义一对值分别为`string`和`number`类型的元组。
```
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ['hello', 10]; // OK
// Initialize it incorrectly
x = [10, 'hello']; // Error`</pre>
```

当访问一个已知索引的元素，会得到正确的类型：
```
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
```
当访问一个越界的元素，会使用联合类型替代：
```
x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型
console.log(x[5].toString()); // OK, 'string' 和 'number' 都有 toString
x[6] = true; // Error, 布尔不是(string | number)类型
```

##枚举
num类型是对JavaScript标准数据类型的一个补充。 像C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。
```
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```
编译出来为
```
var Color;
(function (Color) {
    Color[Color["Red"] = 0] = "Red";
    Color[Color["Green"] = 1] = "Green";
    Color[Color["Blue"] = 2] = "Blue";
})(Color || (Color = {}));
var c = Color.Green;
```
默认从0开始，也可以手动指定
```
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green; //1
//编译出来如下
var Color;
(function (Color) {
    Color[Color["Red"] = 1] = "Red";
    Color[Color["Green"] = 2] = "Green";
    Color[Color["Blue"] = 3] = "Blue";
})(Color || (Color = {}));
var c = Color.Green; //2

console.log(Color)//{1: "Red", 2: "Green", 3: "Blue", Red: 1, Green: 2, Blue: 3}
```
也可以全部手动赋值

##Any
有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。 那么我们可以使用 any类型来标记这些变量：
```
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

##Void
某种程度上来说，`void`类型像是与`any`类型相反，它表示没有任何类型。 当一个**函数没有返回值时**，你通常会见到其返回值类型是 `void`：
```
function warnUser(): void {
    console.log("This is my warning message");
}
```
声明一个`void`类型的变量没有什么大用，因为你只能为它赋予`undefined`和`null`：
```
let unusable: void = undefined;
```
##Never
never类型表示的是那些永不存在的值的类型。 例如， never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是 never类型，当它们被永不为真的类型保护所约束时。

never类型是任何类型的子类型，也可以赋值给任何类型；然而，没有类型是never的子类型或可以赋值给never类型（除了never本身之外）。 即使 any也不可以赋值给never。

下面是一些返回never类型的函数：
```
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```
参考链接
[typescript官方文档](https://www.tslang.cn/docs/handbook/basic-types.html)