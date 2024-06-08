---
title: 语句
---

我们不仅可以声明响应式 _变量_，还可以直接运行响应式 _语句_。比如说，我们可以在 `count` 变量变更时打印其值：

```js
/// file: App.svelte
let count = 0;

+++$: console.log(`the count is ${count}`);+++
```

你也可以使用代码块来包含多条语句：

```js
/// file: App.svelte
$: +++{+++
	console.log(`the count is ${count}`);
	console.log(`this will also be logged whenever count changes`);
+++}+++
```

你也可以在 `if` 代码块之前添加 `$:` ：

```js
/// file: App.svelte
$: +++if (count >= 10)+++ {
	alert('count is dangerously high!');
	count = 0;
}
```
