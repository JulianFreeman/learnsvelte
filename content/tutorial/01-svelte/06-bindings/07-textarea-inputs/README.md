---
title: 文本域输入
---

在 Svelte 中，`textarea` 元素跟文本输入差不多，用 `bind:value`：

```svelte
/// file: App.svelte
<textarea +++bind:value=+++{value}></textarea>
```

在这种情况，属性和变量的名称相同，也可以简写：

```svelte
/// file: App.svelte
<textarea +++bind:value+++></textarea>
```

这种简写对于所有绑定都适用，不只是 `textarea`。
