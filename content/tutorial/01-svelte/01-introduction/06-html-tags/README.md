---
title: HTML 标签
---

一般来说，字符串都是纯文本文字，也就是说像 `<` 和 `>` 这种字符是没有特殊含义的。

但是有时候你可能需要直接在组件中渲染 HTML。比如说，现在你正在阅读的文字就包含在一个 Markdown 文件中，然后作为一段 HTML 被插入到当前页面中。

在 Svelte 中，你可以通过一个特殊的 `{@html ...}` 标签来实现这点：

```svelte
/// file: App.svelte
<p>{+++@html+++ string}</p>
```

> **注意**，Svelte 并不会对 `{@html ...}` 中的代码进行任何安全检查。如果这些代码是你自己写的，那自然没什么问题，但如果是其他不可信任的用户内容，比如用户的评论，你就需要手动处理一下，以免遭受 <a href="https://owasp.org/www-community/attacks/xss/" target="_blank">XSS</a> 攻击。
