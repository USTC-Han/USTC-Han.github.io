---
title: js交换两个变量
tags: 
- JS
- 变量互换
toc: true
---
## 前言
这个题目是一道大厂的面试题(我不喜欢这个题)，要求用尽量多的方式实现两个变量互换，此处做个总结。

## 推荐写法
### 中间值法
```js
var t = a;
a = b;
b = t
```
虽然这个写法比较累赘，但是这种写法是最易读的，无论JS开发人员，还是其它语言的使用者，都可以看懂。

### ES6结构赋值
```js
  let a = "one",b = "two";
  [a, b] = [b, a];
  console.log(a, b);//two one
```
利用ES6语法实现两值交换相比上一种写法简单好多，也是我比较喜欢的一种写法，包括在React hook中的useState也是这种写法。
```js
[count, setCount] = useState(0)
```
<!--more-->
## 骚操作
### 公式法：
```js
a=[b,b=a][0]
```
这种写法，现将b的值存在了数组的第一个位置，然后让在数组第二个位置做了b =a的赋值操作，让b拿到了a的值，再通过取数组的第一和值给a,让a拿到之前b的值。

我不喜欢这个写法，它虽然让人看着简单，但可读性太差。

### 异或法(number)
```js
a = a^b;
b = a^b;
a = a^b;
```
因为a = a^b，所以b = a^b = a^(b^b) = a
第三步：因为a = a^b，由上步b = a，所以a = a^b = (a^b) ^ a = (a^a)^b = b

其实这个很简单，利用异或的方式来实现a和b的交换

### 和差法(number)
```js
a = a+b;
b = a - b;
a = a - b;
```
第二步之前好理解，第二步的时候，b = a; 第三步 a = a -b = (a+b) -a = b

## 小结
写法有很多，但是可读性第一，代码量第二，项目中最好不要使用骚操作。假如代码写错了，同事review代码可以帮我们看出来，避免不必要的bug出现。