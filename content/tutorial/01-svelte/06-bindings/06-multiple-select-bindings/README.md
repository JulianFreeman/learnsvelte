---
title: 多选
---

`select` 元素可以有 `multiple` 属性，开启后返回值是一个数组而非单个值。

用 `<select multiple>` 替换复选框：

```svelte
/// file: App.svelte
<h2>Flavours</h2>

+++<select multiple bind:value={flavours}>+++
	{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
+++		<option>{flavour}</option>+++
	{/each}
+++</select>+++
```

注意如果 `option` 元素内的内容与 `value` 属性的值相同，则可以省略 `value` 属性。

> 按住 `CTRL` 键（MacOS 上的 `command` 键）可以选择多个选项。
