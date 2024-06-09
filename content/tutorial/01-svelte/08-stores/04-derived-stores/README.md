---
title: 派生存储
---

你可以用 `derived` 函数创建一个依赖于 _其他_ 一个或多个 store 的 store。接续上一个例子，我们可以创建一个 store，派生自页面打开的时间：

```js
/// file: stores.js
export const elapsed = derived(
    time,
    ($time) => +++Math.round(($time - start) / 1000)+++
);
```

> 也可以从多个输入 stores 中派生一个 store，然后显式地用 `set` 来设定其值而不是简单地返回（这在异步派生值的时候很有用）。查看 [API 参考](https://svelte.dev/docs#run-time-svelte-store-derived) 获取更多信息。
