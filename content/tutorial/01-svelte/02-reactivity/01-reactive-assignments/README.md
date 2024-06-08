---
title: 赋值
---

Svelte 的核心是一个强大的 *响应* 系统，用来保持 DOM 跟应用状态同步。比如说响应事件。

要演示这个，我们首先需要创建一个事件处理器（我们会在 [稍后](/tutorial/dom-events) 学习这个）：

```svelte
/// file: App.svelte
<button +++on:click={increment}+++>
	Clicked {count}
	{count === 1 ? 'time' : 'times'}
</button>
```

在 `increment` 函数内，我们只需要更改 `count` 的值即可：

```js
/// file: App.svelte
function increment() {
	+++count += 1;+++
}
```

Svelte 会把这个赋值“构建”成一些代码，来通知 DOM 它需要更新了。
