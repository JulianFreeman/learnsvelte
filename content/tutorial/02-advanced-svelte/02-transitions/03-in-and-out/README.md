---
title: in 和 out 标志
---

除了 `transition` 标志，一个元素也可以有 `in` 和/或 `out` 标志。在 `fly` 旁边导入 `fade` ……

```js
/// file: App.svelte
import { +++fade+++, fly } from 'svelte/transition';
```

……然后用分开的 `in` 和 `out` 标志替换 `transition` 标志：

```svelte
/// file: App.svelte
<p +++in+++:fly={{ y: 200, duration: 2000 }} +++out:fade+++>
	Flies in, +++fades out+++
</p>
```

在这种情况下，过渡是 _不_ 可逆的。
