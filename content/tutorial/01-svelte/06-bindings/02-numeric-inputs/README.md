---
title: 数字输入
---

在 DOM 中，一切皆为字符串。但这对于处理数字来说并不友好，比如 `type="number"` 或者 `type="range"` ，因为你必须记得要先强转 `input.value` 才能用。

但是有了 `bind:value`，Svelte 就帮你处理了：

```svelte
/// file: App.svelte
<label>
	<input type="number" +++bind:+++value={a} min="0" max="10" />
	<input type="range" +++bind:+++value={a} min="0" max="10" />
</label>

<label>
	<input type="number" +++bind:+++value={b} min="0" max="10" />
	<input type="range" +++bind:+++value={b} min="0" max="10" />
</label>
```
