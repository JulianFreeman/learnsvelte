---
title: class 标志的简写
---

一般来说，类跟其对应变量的名称都是相同的：

```svelte
/// no-file
<button
	class="card"
	class:flipped={flipped}
	on:click={() => flipped = !flipped}
>
```

在这种情况下我们可以使用简写形式：

```svelte
/// file: App.svelte
<button
	class="card"
	+++class:flipped+++
	on:click={() => flipped = !flipped}
>
```
