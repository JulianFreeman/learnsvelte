---
title: DOM 事件
---

我们之前已经见过了，你可以通过在元素上加一个 `on:` 标志来监听任何 DOM 事件（比如点击事件或者 [鼠标移动事件](https://developer.mozilla.org/en-US/docs/Web/API/Element/pointermove_event) 等）：

```svelte
/// file: App.svelte
<div +++on:pointermove={handleMove}+++>
	The pointer is at {m.x} x {m.y}
</div>
```
