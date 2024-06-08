---
title: 事件修饰器
---

可以用 _修饰器_ 来调整 DOM 事件处理器的行为。比如说，一个拥有 `once` 修饰器的处理器只会运行一次：

```svelte
/// file: App.svelte
<button on:click+++|once+++={() => alert('clicked')}>
	Click me
</button>
```

下面是所有的修饰器：

- `preventDefault` - 在运行处理器之前调用 `event.preventDefault()`，对于在客户端处理表单会有用
- `stopPropagation` - 调用 `event.stopPropagation()` 阻止事件达到下一个元素
- `passive` - 在触屏或者滚轮事件中提升滚动性能（Svelte 会在可行的时候自动加上这个）
- `nonpassive` - 显式地设置 `passive: false`
- `capture` - 在 [_事件捕获_](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_capture) 期触发处理器，而不是 [_事件冒泡_](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling) 期
- `once` - 在第一次运行后移除该处理器
- `self` - 只有在 `event.target` 是元素自身时才触发处理器
- `trusted` - 只有当 `event.isTrusted` 是 `true` 才触发处理器，这意味着事件只会被用户行为触发，而不会被形如 `element.dispatchEvent(...)` 的 JavaScript 代码触发

你也可以同时使用多个修饰器，比如：`on:click|once|capture={...}` 。
