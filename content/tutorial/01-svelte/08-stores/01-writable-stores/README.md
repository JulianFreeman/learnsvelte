---
title: 可写存储
---

并不是所有的应用状态都存在于应用的组件结构中。有的值需要被多个互不相关的组件使用，或者被常规的 JavaScript 模块使用。

在 Svelte 中，我们通过 _存储_ （stores）实现这点。一个 store 就是一个带有 `subscribe` 方法的对象，当存储的值发生变化时用来通知感兴趣的订阅方。在 `App.svelte` 中，`count` 就是一个 store，我们在 `count.subscribe` 的回调函数中设置 `count_value` 的值。

打开 `stores.js` 查看 `count` 的定义。这是一个 _可写_ 存储，表示除了 `subscribe` 方法之外，它还有 `set` 和 `update` 方法。

现在，在 `Incrementer.svelte` 中，修改函数让 `+` 按钮起作用：

```js
/// file: Incrementer.svelte
function increment() {
	+++count.update((n) => n + 1);+++
}
```

现在点击 `+` 按钮就会更新 `count` 了。同理修改 `Decrementer.svelte`。

最后，在 `Resetter.svelte` 中，实现 `reset`：

```js
/// file: Resetter.svelte
function reset() {
	+++count.set(0);+++
}
```
