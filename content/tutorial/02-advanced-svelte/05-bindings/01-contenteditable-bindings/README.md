---
title: 可编辑内容绑定
---

支持 `contenteditable` 属性的元素可以使用 `textContent` 和 `innerHTML` 绑定：

```svelte
/// file: App.svelte
<div +++bind:innerHTML={html}+++ contenteditable></div>
```
