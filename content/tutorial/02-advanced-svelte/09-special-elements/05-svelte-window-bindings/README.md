---
title: <svelte:window> 绑定
---

我们也可以绑定到 `window` 的特定属性上，比如 `scrollY`：

```svelte
/// file: App.svelte
<svelte:window +++bind:scrollY={y}+++ />
```

下面是你可以绑定到的属性的列表：

- `innerWidth`
- `innerHeight`
- `outerWidth`
- `outerHeight`
- `scrollX`
- `scrollY`
- `online` — `window.navigator.onLine` 的别名

除了 `scrollX` 和 `scrollY` 之外都是只读的。
