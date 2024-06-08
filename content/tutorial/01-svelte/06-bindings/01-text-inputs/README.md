---
title: 文本输入
---

一般来说，Svelte 中的数据流是 _自上而下_ 的，比如父组件可以给子组件设置属性（props），组件可以给元素设置属性（attributes），反过来就不行。

但有时候我们就是想反过来。拿本例组件中的 `input` 元素为例，我们可以加一个 `on:input` 事件处理器来把 `name` 的值设置为 `event.target.value`，但这样有点……死板了。在其他表单元素中这样的处理更糟，将来我们会见到。

相反，我们可以使用 `bind:value` 标志：

```svelte
/// file: App.svelte
<input +++bind:+++value={name}>
```

这就意味着，修改 `name` 会更新文本框内的值，而修改文本框内的值也会更新 `name` 。
