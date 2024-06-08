---
title: 扩展属性
---

在这个练习中，我们忘记指定 `PackageInfo.svelte` 组件所需要的 `version` 属性了，导致出现了 `version undefined`。

我们 _可以_ 把 `version` 加上来解决这个问题……

```svelte
/// file: App.svelte
<PackageInfo
    name={pkg.name}
	speed={pkg.speed}
    +++version={pkg.version}+++
	website={pkg.website}
/>
```

……但，因为 `pkg` 的属性跟组件所需要的属性是有关联的，因为我们可以把属性“扩展”到子组件中：

```svelte
/// file: App.svelte
<PackageInfo +++{...pkg}+++ />
```

> 反过来，如果你需要在组件内引用所有的属性，包括那些没有添加 `export` 声明的属性，你可以直接用 `$$props`。通常不推荐使用这个，因为这会让 Svelte 很难优化代码，但是在某些情况下这的确有用。
