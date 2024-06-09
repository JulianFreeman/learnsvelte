---
title: <svelte:body>
---

跟 `<svelte:window>` 类似，`<svelte:body>` 元素允许你监听 `document.body` 上发生的事件。这对于 `mouseenter` 和 `mouseleave` 这样的事件来说很有用，因为这些事件不是在 `window` 上的。

向 `<svelte:body>` 标签添加 `mouseenter` 和 `mouseleave` 的处理器……

```svelte
/// file: App.svelte
<svelte:body
	+++on:mouseenter={() => hereKitty = true}+++
	+++on:mouseleave={() => hereKitty = false}+++
/>
```

……然后将鼠标移动到 `<body>` 上。