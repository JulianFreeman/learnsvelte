---
title: Key 代码块
---

Key 代码块会在表达式的值变更时销毁并重新创建其内容。如果你希望一个元素会在其值变更时产生过渡效果，而不仅仅在其加入或者离开 DOM 时产生，那么这个就很有用。

比如说，我们希望每当加载信息，也就是 `i` 的值发生变动时，就播放 `transition.js` 文件的 `typewriter` 过渡。把 `p` 元素包裹在一个 key 代码块中：

```svelte
/// file: App.svelte
+++{#key i}+++
	<p in:typewriter={{ speed: 10 }}>
		{messages[i] || ''}
	</p>
+++{/key}+++
```