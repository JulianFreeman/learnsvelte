---
title: <svelte:self>
---

Svelte 提供了一系列的内置元素。第一个元素，`<svelte:self>`，允许一个组件递归地包含自己。

这对于处理像文件树结构之类的东西很有用，目录里会包含 _其他_ 目录。在 `Folder.svelte` 中我们如果这样做……

```svelte
/// file: Folder.svelte
{#if file.files}
	<Folder {...file}/>
{:else}
	<File {...file}/>
{/if}
```

……是行不通的，因为一个模块不能导入自己。因此，我们可以使用 `<svelte:self>`：

```svelte
/// file: Folder.svelte
{#if file.files}
	+++<svelte:self {...file} />+++
{:else}
	<File {...file} />
{/if}
```
