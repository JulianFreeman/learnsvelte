---
title: <svelte:window>
---

就如同你可以给任意 DOM 元素添加事件监听器一样，你也可以通过 `<svelte:window>` 给 `window` 对象添加事件监听器。

我们已经有一个 `handleKeydown` 函数了，现在要做的就是添加一个 `keydown` 监听器：

```svelte
/// file: App.svelte
<svelte:window +++on:keydown={handleKeydown}+++ />
```

> 如同 DOM 元素一样，你可以添加 `preventDefault` 这样的 [事件修饰器](/tutorial/event-modifiers)。
