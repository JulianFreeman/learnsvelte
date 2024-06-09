---
title: animate 标志
---

在 [上一章](/tutorial/deferred-transitions) 中，我们使用延迟过渡创建了一个列表元素从一个表移动到另一个表的运动效果。

要完成这个效果，我们还需要对剩下的 _不_ 过渡的元素应用运动效果。要达到这一点，我们使用 `animate` 标志。

首先，在 `TodoList.svelte` 中，从 `svelte/animate` 导入 `flip` 函数，flip 代表 ['First, Last, Invert, Play'](https://aerotwist.com/blog/flip-your-animations/)：

```svelte
/// file: TodoList.svelte
<script>
	+++import { flip } from 'svelte/animate';+++
	import { send, receive } from './transition.js';

	export let store;
	export let done;
</script>
```

然后添加到 `li` 元素上：

```svelte
/// file: TodoList.svelte
<li
	class:done
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	+++animate:flip+++
>
```

现在运动得有一点慢，我们可以加一个 `duration` 参数：

```svelte
/// file: TodoList.svelte
<li
	class:done
	in:receive={{ key: todo.id }}
	out:send={{ key: todo.id }}
	animate:flip+++={{ duration: 200 }}+++
>
```

> `duration` 也可以是一个 `d => milliseconds` 函数，其中 `d` 是元素要移动的像素个数

注意所有的过渡和动画都是由 CSS 完成的，而非 JavaScript，因此它们不会阻断主线程或者被主线程阻断。
