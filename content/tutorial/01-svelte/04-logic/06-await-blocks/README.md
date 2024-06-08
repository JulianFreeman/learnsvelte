---
title: Await 代码块
---

大部分网页应用都需要处理异步数据。Svelte 可以让你很容易地直接在标记（markup）中 _等待_ [promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises) 的值。

```svelte
/// file: App.svelte
+++{#await promise}+++
	<p>...waiting</p>
+++{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}+++
```

> 只有最新的 `promise` 会被考虑，因此你不用担心竞争条件。

如果你确定你的 promise 不会被拒绝，那么可以省略 `catch` 代码块。如果你也不需要展示等待的状态，也可以省略第一个块，直接等到 promise 有结果之后再展示：

```svelte
/// no-file
{#await promise then number}
	<p>The number is {number}</p>
{/await}
```
