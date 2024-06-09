---
title: <svelte:options>
---

`<svelte:options>` 元素允许你指定编译器选项。

我们这里选择 `immutable` 选项举例。在本例中，每当 `<Todo>` 组件接收到新数据时都会闪一下。单击任意一个元素的复选框都会变更 `done` 的状态，从而导致 `todos` 数组发生更新。这样会导致 _其他_ `<Todo>` 组件也发生闪动，尽管它们的 DOM 并没有发生任何变动。

我们可以通过告知 `<Todo>` 组件接收 _不可变_ 数据来优化这点。这个的意思是，我们保证永远不会 _变动_ `todo` 这个属性，而是在每次发生变动的时候创建新的 `todo` 对象。

将这行添加到 `Todo.svelte` 顶端：

```svelte
/// file: Todo.svelte
<svelte:options immutable={true} />
```

> 如果你喜欢，也可以把这行简写作 `<svelte:options immutable/>`。

现在，当你点击复选框时，只有被更新的组件会闪动了。

可以被设定的选项如下：

- `immutable={true}` — 你永远不会使用可变的数据，因此编译器通过简单的引用对等检查来判断值是否发生变化
- `immutable={false}` — 默认。Svelte 对于可变对象是否发生改变的检查会更保守谨慎一些
- `accessors={true}` — 给组件的属性（props）添加 getter 和 setter
- `accessors={false}` — 默认
- `namespace="..."` — 该组件被使用的命名空间，通常是 `"svg"`
- `customElement="..."` — 将该组件编译为自定义元素时使用的名称

查看 [API 参考](https://svelte.dev/docs) 获取更多关于这些选项的信息。
