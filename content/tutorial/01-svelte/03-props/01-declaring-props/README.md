---
title: 声明属性
---

目前为止，我们只处理了组件的内部状态，也就是说，这些值只在组件内部可用。

但在实际的应用场景中，你可能会需要把数据从一个组件向下传递到其子组件中。要实现这点，我们需要声明 _属性_（properties），简写作 `props` 。在 Svelte 中，我们使用 `export` 关键字。将 `Nested.svelte` 组件修改如下：

```svelte
/// file: Nested.svelte
<script>
	+++export+++ let answer;
</script>
```

> 就像 `$:` 一样，一开始你可能会感觉有点奇怪，因为这不是 `export` 在 JavaScript 模块中的常规用法。就先接受过来吧，之后就习惯了。
