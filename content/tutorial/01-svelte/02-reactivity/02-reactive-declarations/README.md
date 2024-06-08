---
title: 声明
---

当组件状态更改时，Svelte 会自动通知 DOM 更新。但有时候，有些组件的状态是通过 _其他_ 部分计算出来的，比如 `fullname` 是由 `firstname` 和 `lastname` 合并出来的。当其中某一部分变更时，它们都需要重新计算。

对于这种情况，我们有 _响应式声明_，长这样：

```js
/// file: App.svelte
let count = 0;
+++$: doubled = count * 2;+++
```

如果一个响应式语句只包含对一个未声明变量的赋值，那么 Svelte 会自动加一个 `let`。

> 如果这看上去有点奇怪，不要想太多，这其实是 [合法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label) （但可能不太常见）的 JavaScript 语法。对于 Svelte 来说，这个语法的含义就是每当被引用的值更改时，就重新计算。习惯就好。

让我们在标记中用一下这个 `doubled` ：

```svelte
/// file: App.svelte
<button>...</button>

+++<p>{count} doubled is {doubled}</p>+++
```

当然了，对于这个例子来说，你大可以直接写 `{count * 2}`，根本用不着什么响应式。但是响应式变量在某些情况下会很有用，比如你需要多次引用一个计算出来的值，或者你的变量依赖于 _其他_ 响应式变量。

> 响应式的声明和语句会在其他脚本代码运行完毕之后，组件标记代码渲染之前运行。
