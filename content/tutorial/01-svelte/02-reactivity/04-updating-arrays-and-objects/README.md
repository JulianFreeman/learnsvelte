---
title: 更新数组和对象
---

因为 Svelte 的响应是由赋值触发的，所以使用 `push` 或 `splice` 这样的数组方法不会自动触发更新。比如，尽管我们在 `addNumber` 函数内调用了 `numbers.push(...)`，但点击 Add a number 按钮什么都不会发生。

其中一个解决这个问题的办法是写一个冗余的赋值：

```js
/// file: App.svelte
function addNumber() {
	numbers.push(numbers.length + 1);
	+++numbers = numbers;+++
}
```

但是还有一个更常用的办法是这样：

```js
/// file: App.svelte
function addNumber() {
	numbers = +++[...numbers, numbers.length + 1];+++
}
```

你可以用类似的模式替换 `pop`，`shift`，`unshift` 和 `splice` 。

对数组或者对象的 _属性_ （properties）的赋值也可以触发更新，比如 `obj.foo += 1` 或者 `array[i] = x` 等。

```js
/// file: App.svelte
function addNumber() {
	numbers[numbers.length] = numbers.length + 1;
}
```

一条简单的经验法则：要更新的值的名字必须出现在赋值的左边才行。比如说下面这个……

```js
/// no-file
const obj = { foo: { bar: 1 } };
const foo = obj.foo;
foo.bar = 2;
```

……就不会触发 `obj.foo.bar` 的更新，除非你接一条 `obj = obj`。
