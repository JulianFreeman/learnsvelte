---
title: Else-if 代码块
---

可以使用 `else if` 连接多个条件：

```svelte
/// file: App.svelte
{#if count > 10}
	<p>{count} is greater than 10</p>
+++{:else if count < 5}
	<p>{count} is less than 5</p>+++
{:else}
	<p>{count} is between +++5+++ and 10</p>
{/if}
```
