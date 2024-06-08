---
title: 内联事件处理器
---

你也可以直接在标记内声明事件处理器：

```svelte
/// file: App.svelte
<script>
	let m = { x: 0, y: 0 };

	---function handleMove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}---
</script>

<div
	on:pointermove={+++(e) => {
		m = { x: e.clientX, y: e.clientY };
	}+++}
>
	The pointer is at {m.x} x {m.y}
</div>
```

> 在一些其他框架中，你可能会见到说不建议使用内联事件处理器，尤其在循环中，因为会影响性能。这个对 Svelte 不适用，因为编译器总是会做最正确的事情，不管你怎么写。
