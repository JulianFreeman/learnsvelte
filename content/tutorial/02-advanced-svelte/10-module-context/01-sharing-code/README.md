---
title: 共享代码
---

在我们目前为止的例子中，`script` 标签内的代码会在每个组件实例初始化时运行一次。对于大部分的组件，这就是我们想要的。

极少的情况下，你会需要在单个的组件实例之外运行一些代码。比如说，拿我们 [之前一节](media-elements) 中的音乐播放器来说，你可以同时播放所有的音乐。但如果播放一个能自动暂停其他的音乐，会更好。

我们可以通过声明一个 `<script context="module">` 代码块来实现这点。在这里面包含的代码只会在该模块第一次解析时运行一次，而不是每创建一个组件就运行一次。把这个放在 `AudioPlayer.svelte` 的顶端（注意这是一个 _单独的_ 	`script` 标签）：

```svelte
/// file: AudioPlayer.svelte
+++<script context="module">
	let current;
</script>+++
```

现在这几个组件之间不需要任何状态管理也可以相互通信了：

```svelte
/// file: AudioPlayer.svelte
<audio
	src={src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	on:play={(e) => {
		const audio = e.currentTarget;

		if (audio !== current) {
			current?.pause();
			current = audio;
		}
	}}+++
	on:ended={() => {
		time = 0;
	}}
/>
```
