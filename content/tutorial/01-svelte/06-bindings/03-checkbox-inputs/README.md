---
title: 复选框输入
---

复选框用于切换状态，因此我们绑定到 `input.checked` 而非 `input.value`：

```svelte
/// file: App.svelte
<input type="checkbox" +++bind:+++checked={yes}>
```
