---
title: <svelte:document>
---

`<svelte:document>` 元素允许你监听来自 `document` 的事件。这对于像 `selectionchange` 这样的事件很有用，因为同样不来自 `window`。

向 `<svelte:document>` 标签添加 `selectionchange` 处理器：

```svelte
/// file: App.svelte
<svelte:document +++on:selectionchange={handleSelectionChange}+++ />
```

> 不要在这个元素上添加 `mouseenter` 和 `mouseleave` 处理器，因为没有浏览器上的这些事件是在 `document` 上发生的，改用 `<svelte:body>`。
