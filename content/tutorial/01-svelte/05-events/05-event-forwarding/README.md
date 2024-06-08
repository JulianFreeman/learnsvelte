---
title: 事件转发
---

跟 DOM 事件不同，组件事件不会 _冒泡_。如果你想监听更深层嵌套的组件的事件，就得让中间组件来 _转发_ 事件。

在本例中，我们有跟 [上一节](/tutorial/component-events) 中相同的 `App.svelte` 和 `Inner.svelte` 文件，但是现在 `<Inner/>` 被嵌套在 `Outer.svelte` 组件中。

其中一个 _可以_ 解决问题的办法是在 `Outer.svelte` 中添加 `createEventDispatcher`，来监听 `message` 事件，然后创建处理器来处理：

```svelte
/// file: Outer.svelte
<script>
	import Inner from './Inner.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function forward(event) {
		dispatch('message', event.detail);
	}
</script>

<Inner on:message={forward}/>
```

但这样要写老多代码，因此 Svelte 允许我们使用简写：一个没有值的事件标志 `on:message` 表示转发所有 `message` 事件。

```svelte
/// file: Outer.svelte
<script>
	import Inner from './Inner.svelte';
</script>

<Inner +++on:message+++/>
```
