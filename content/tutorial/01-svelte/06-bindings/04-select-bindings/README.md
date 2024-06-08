---
title: 选择绑定
---

我们也可以在 `select` 元素上使用 `bind:value`：

```svelte
/// file: App.svelte
<select
    +++bind:+++value={selected}
    on:change={() => answer = ''}
>
```

注意 `option` 元素的值是对象，而不是字符串，不过 Svetle 并不在意。

> 因为我们没有给 `selected` 设置初始值，所以绑定会自动设置一个默认值，也就是列表的第一个值。但是要注意，在绑定初始化之前，`selected` 一直是未定义的，所以我们不能盲目地使用 `selected.id` 。（在最后的 `p` 元素中要加一个判断）
