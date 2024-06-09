---
title: 尺寸
---

每一格块级别的元素都有 `clientWidth`、`clientHeight`、`offsetWidth` 和 `offsetHeight` 这几个绑定：

```svelte
/// file: App.svelte
<div +++bind:clientWidth={w} bind:clientHeight={h}+++>
	<span style="font-size: {size}px" contenteditable>{text}</span>
	<span class="size">{w} x {h}px</span>
</div>
```

这些绑定都是只读绑定，修改 `w` 和 `h` 的值不会对元素造成任何影响。

> Svelte 使用类似 [这样](http://www.backalleycoder.com/2013/03/18/cross-browser-event-based-element-resize-detection/) 的方法获取元素的尺寸，这会涉及到一些开销，因此不建议在大量的元素上使用这个。
>
> `display: inline` 的元素无法使用这种办法获取尺寸，不能包含其他元素的元素（比如 `canvas`）也不行。在这种情况下你需要先用一个包装元素把元素包起来再获取包装元素的尺寸。
