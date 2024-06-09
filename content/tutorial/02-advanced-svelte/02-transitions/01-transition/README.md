---
title: transition 标志
---

我们可以通过更加优雅地将元素加入和移除 DOM，来构建更吸引人的用户界面。Svelte 提供了 `transition` 标志，使得这样的效果很容易达到。

首先，从 `svelte/transition` 中导入 `fade` 函数……

```svelte
/// file: App.svelte
<script>
	+++import { fade } from 'svelte/transition';+++
	let visible = true;
</script>
```

……然后把它加到 `p` 元素中：

```svelte
/// file: App.svelte
<p +++transition:fade+++>
	Fades in and out
</p>
```
