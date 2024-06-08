---
title: 组件事件
---

组件也可以派发事件。要实现这点，我们必须创建一个事件派发器。更新 `Inner.svelte`：

```svelte
/// file: Inner.svelte
<script>
	+++import { createEventDispatcher } from 'svelte';+++

	+++const dispatch = createEventDispatcher();+++

	function sayHello() {
		dispatch('message', {
			text: 'Hello!'
		});
	}
</script>
```

> `createEventDispatcher` 必须在组件首次初始化时调用，而不能在之后调用（比如在 `setTimeout` 回调中）。这样才能把 `dispatch` 跟组件实例连接起来。

然后在 `App.svelte` 中添加 `on:message` 处理器：

```svelte
/// file: App.svelte
<Inner +++on:message={handleMessage}+++ />
```

> 你也可以把事件名称换成别的，比如在 `Inner.svelte` 中把 `dispatch('message', {...})` 换成 `dispatch('greet', {...})`，然后在 `App.svelte` 中把 `on:message` 换成 `on:greet`。
