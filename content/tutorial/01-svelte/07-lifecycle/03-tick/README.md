---
title: tick
---

`tick` 函数不同于其他的生命周期函数，你可以在任意时刻调用它，而不必一定在组件初始化时。它会返回一个 promise，并在任意待处理的状态变更应用到 DOM 之后产生结果（resolve），或者立刻产生结果，如果没有任何待处理的状态变更的话。

当你在 Svelte 中更新组件的时候，DOM 不会立刻更新。相反，它会先看看是否有其他组件的其他变更需要被应用，然后等到下一个 _微任务_ 再处理。这样做可以避免一些无用功，并且让浏览器可以更高效地批量处理事情。

你可以在本例中看到这种现象。选中一定范围的文本，然后敲击 tab 键，因为 `textarea` 元素内的值更改了，因此当前的选中状态被清除了，光标也跳到了最后，就挺烦人的。我们可以引入 `tick` 来解决这点……

```js
/// file: App.svelte
+++import { tick } from 'svelte';+++

let text = `Select some text and hit the tab key to toggle uppercase`;
```

……然后在我们于 `handleKeydown` 函数结尾设置 `this.selectionStart` 和 `this.selectionEnd` 之前调用：

```js
/// file: App.svelte
+++await tick();+++
this.selectionStart = selectionStart;
this.selectionEnd = selectionEnd;
```
