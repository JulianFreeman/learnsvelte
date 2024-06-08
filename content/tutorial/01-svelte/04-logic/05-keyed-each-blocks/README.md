---
title: 带键值的 Each 代码块
---

默认来说，当你修改 `each` 代码块的值时，Svelte 会在代码块的 _结尾_ 添加或者移除 DOM 节点，然后更新任何变更的值。有时候这不是你想要的。

原因很简单，`Thing` 组件的 `emoji` 是在初始化时固定的，而 `name` 是作为属性（prop）传进去的。

多点几次 Remove first thing 按钮，观察发生了什么：

1. 移除了最后一个组件。
2. 对剩余的 DOM 节点更新了 `name` 属性，但没有更新 `emoji`，因为它在组件创建时就定死了。

实际上，我们希望只移除第一个 `Thing` 组件和它对应的 DOM 节点，而保持剩下的不动。

要实现这一点，我们需要在 `each` 代码块的每一次迭代中指定一个唯一的标识符（一个 key）：

```svelte
/// file: App.svelte
{#each things as thing (+++thing.id+++)}
	<Thing name={thing.name}/>
{/each}
```

在这里，`(thing.id)` 就是那个 _key_，它用于帮助 Svelte 分辨出当值（此例中的 `name`）发生变化的时候，应该更新哪个。

> 你可以使用任何对象作为 key，因为 Svelte 在内部使用 `Map` 实现该功能。也就是说，你也可以使用 `(thing)` 而非 `(thing.id)` 作为 key。使用字符串或者数字更保险一点，因为 it means identity persists without referential equality, for example when updating with fresh data from an API server.
