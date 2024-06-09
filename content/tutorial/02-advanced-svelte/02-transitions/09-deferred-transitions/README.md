---
title: 延迟过渡
---

Svelte 过渡引擎的一个特别强大的特性是允许我们 _延迟_ 过渡，因此在多个元素之间可以达到协调配合。

拿这两个待办列表为例，点击复选框就会把该项转移到另一个列表中。在现实世界中，物体并不是这样突然从一个地方消失又突然从另一个地方出现的，相反它们会经过一段连续的位置移动过去。使用运动效果可以大大帮助用户了解你的应用中发生了什么。

我们可以使用 `transition.js` 中的 `crossfade` 函数实现这点，该函数会创建两个叫 `send` 和 `receive` 的过渡函数。当一个元素被发送的时候，它会找到那个与之相对的要被接收的元素，然后生成一段从自己的位置移动到对方位置的动画并渐渐消失。当一个元素被接收时，就反过来。如果没有找到对应的元素，就会调用 `fallback` 过渡。

打开 `TodoList.svelte`，首先从 transition.js 导入 `send` 和 `receive` 两个过渡函数：

```svelte
/// file: TodoList.svelte
<script>
	+++import { send, receive } from './transition.js';+++

	export let store;
	export let done;
</script>
```

然后把它们加入到 `li` 元素中，使用 `todo.id` 属性作为 key 来匹配元素：

```svelte
/// file: TodoList.svelte
<li
	class:done
	+++in:receive={{ key: todo.id }}+++
	+++out:send={{ key: todo.id }}+++
>
```

现在，当你点击复选框时，列表元素会平滑地移动到新位置。剩下不移动的元素没有过渡效果，依然会很难看地跳来跳去，我们在下一章中解决这个问题。
