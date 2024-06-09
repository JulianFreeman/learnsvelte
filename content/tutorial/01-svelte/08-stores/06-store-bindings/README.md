---
title: 存储绑定
---

如果一个 store 是可写的，也就是说它拥有 `set` 方法，你就可以绑定其值，就如同绑定一个本地的组件状态一样。

在本例中，我们从 `stores.js` 文件中导出了一个可写存储 `name` 和一个派生存储 `greeting`。在 `App.svelte` 中更新 `input` 元素：

```svelte
/// file: App.svelte
<input +++bind:+++value={$name}>
```

现在修改输入框的值将会更新 `name` 以及其依赖。

我们也可以直接在组件内给 store 的值赋值。添加一个 `on:click` 事件处理器来更新 `name`：

```svelte
/// file: App.svelte
<button +++on:click={() => $name += '!'}+++>
	Add exclamation mark!
</button>
```

`$name += '!'` 赋值等同于 `name.set($name + '!')`。
