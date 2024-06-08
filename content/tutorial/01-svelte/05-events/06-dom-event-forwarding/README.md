---
title: DOM 事件转发
---

DOM 事件也可以用同样的简写转发。

如果我们想监听 `<BigRedButton>` 中的点击事件，只需要把 `BigRedButton.svelte` 中的 `button` 元素的 `click` 事件转发出去即可：

```svelte
/// file: BigRedButton.svelte
<button +++on:click+++>
	Push
</button>
```
