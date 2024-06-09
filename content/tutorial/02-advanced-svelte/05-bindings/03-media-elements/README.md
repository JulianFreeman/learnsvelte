---
title: 媒体元素
---

你可以绑定 `<audio>` 和 `<video>` 元素的属性，以轻松构建自定义的播放器 UI，就像 `AudioPlayer.svelte` 一样。

首先，添加 `audio` 元素及其绑定（我们使用 `src`、`duration` 和 `paused` 的简写形式）：

```svelte
/// file: AudioPlayer.svelte
<div class="player" class:paused>
+++	<audio
		{src}
		bind:currentTime={time}
		bind:duration
		bind:paused
	></audio>+++

	<button
		class="play"
		aria-label={paused ? 'play' : 'pause'}
	></button>
```

然后，给 `button` 添加一个事件处理器，用来切换 `paused`：

```svelte
/// file: AudioPlayer.svelte
<button
	class="play"
	aria-label={paused ? 'play' : 'pause'}
	+++on:click={() => paused = !paused}+++
></button>
```

现在我们的音乐播放器已经有基本的功能了。再让我们添加可以拖动滑块将音乐定位到指定时长的功能。在滑块的 `pointerdown` 处理器中有一个 `seek` 函数，我们可以在里面更新 `time`：

```js
/// file: AudioPlayer.svelte
function seek(e) {
	const { left, width } = div.getBoundingClientRect();

	let p = (e.clientX - left) / width;
	if (p < 0) p = 0;
	if (p > 1) p = 1;

	+++time = p * duration;+++
}
```

当音乐播放完毕之后，让我们友好一点，给进度条复位：

```svelte
/// file: AudioPlayer.svelte
<audio
	{src}
	bind:currentTime={time}
	bind:duration
	bind:paused
+++	on:ended={() => {
		time = 0;
	}}+++
></audio>
```

`<audio>` 和 `<video>` 的所有绑定列举如下，一共七个 _只读_ 绑定……

- `duration` （只读） — 总时长，以秒为单位
- `buffered` （只读） — 一个包含 `{start, end}` 对象的数组
- `seekable` （只读） — 同上
- `played` （只读） — 同上
- `seeking` （只读） — 布尔
- `ended` （只读） — 布尔
- `readyState` （只读） — 0 到 4 （包含）之间的数字

……和五个 _双向_ 绑定：

- `currentTime` — 当前播放位置，以秒为单位
- `playbackRate` — 加速或者减速（`1` 是“正常速度”）
- `paused` — 这个应该很好理解
- `volume` — 0 到 1 之间的值
- `muted` — 一个布尔值，`true` 表示静音

视频额外具有 `videoWidth` 和 `videoHeight` 两个只读绑定。
