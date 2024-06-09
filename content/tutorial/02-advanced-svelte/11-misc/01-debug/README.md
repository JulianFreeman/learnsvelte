---
title: @debug 标签
---

有时候，你可能会需要监视一部分数据是怎么在应用中流动的。

其中一个办法是在标记（markup）中用 `console.log(...)`，但如果你想中断执行，你可以使用 `{@debug ...}` 标签，填入你想要监视的变量，以逗号分割。

```svelte
/// file: App.svelte
{@debug user}

<h1>Hello {user.firstname}!</h1>
```

如果现在打开开发者工具，然后更改文本框的内容，当 `user` 的值发生变化的时候，就会触发调试器。（注意本教程的调用栈和局部变量都是不可见的，因为 iframe 的安全限制问题。）
