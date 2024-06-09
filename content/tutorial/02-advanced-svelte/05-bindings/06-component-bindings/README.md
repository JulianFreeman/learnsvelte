---
title: 组件绑定
---

就如同你可以绑定到 DOM 元素的属性一样，你也可以绑定到组件的属性（props）。比如说，我们可以绑定到 `<Keypad>` 组件的 `value` 属性上，就如同它是一个表单元素一样：

```svelte
/// file: App.svelte
<Keypad
	+++bind:value={pin}+++
	on:submit={handleSubmit}
/>
```

现在，当用户在键盘上输入时，父组件中 `pin` 的值会立刻更新。

> 不要用太多组件绑定，因为这样会很难追踪应用的数据流，特别是某些值可能会被多个地方更改时。
