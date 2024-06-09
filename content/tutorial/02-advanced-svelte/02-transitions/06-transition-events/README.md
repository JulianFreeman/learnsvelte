---
title: 过渡事件
---

有时候能知道过渡何时开始何时结束是很有用的，Svelte 派发了这样的事件，你可以像监听任何其他 DOM 事件一样监听它们：

```svelte
/// file: App.svelte
<p
	transition:fly={{ y: 200, duration: 2000 }}
	+++on:introstart={() => status = 'intro started'}
	on:outrostart={() => status = 'outro started'}
	on:introend={() => status = 'intro ended'}
	on:outroend={() => status = 'outro ended'}+++
>
	Flies in and out
</p>
```
