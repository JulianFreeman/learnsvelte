---
title: 导出
---

任何从 `context="module"` 这个 `script` 标签中导出的内容都会变成从模块本身导出的内容。让我们导出一个 `stopAll` 函数：

```svelte
/// file: AudioPlayer.svelte
<script context="module">
	let current;

+++	export function stopAll() {
		current?.pause();
	}+++
</script>
```

现在我们可以在 `App.svelte` 中导入 `stopAll` 了……

```svelte
/// file: App.svelte
<script>
	import AudioPlayer, +++{ stopAll }+++ from './AudioPlayer.svelte';
	import { tracks } from './tracks.js';
</script>
```

……然后在事件处理器中使用：

```svelte
/// file: App.svelte
<div class="centered">
	{#each tracks as track}
		<AudioPlayer {...track} />
	{/each}

+++	<button on:click={stopAll}>
		stop all
	</button>+++
</div>
```

> 没有默认导出，因为组件本身 _就是_ 默认导出。
