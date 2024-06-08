---
title: Else 代码块
---

就像 JavaScript 一样，`if` 代码块中可以有 `else` 代码块：

```svelte
/// file: App.svelte
{#if count > 10}
	<p>{count} is greater than 10</p>
+++{:else}
	<p>{count} is between 0 and 10</p>+++
{/if}
```

> `#` 符号永远标志着 _一个代码块的开始_，`/` 符号永远标志着 _一个代码块的结束_。`:` 符号，就比如 `{:else}` 中的这个，标志着 _代码块的继续_。不用担心，目前为止你已经学完了所有 Svelte 添加到 HTML 中的语法了。
