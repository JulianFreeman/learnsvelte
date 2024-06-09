---
title: 补间
---

现在我们已经了解基础内容了，是时候学习一些高级的 Svelte 技巧了，从 _运动_ 开始吧。

更改一些值并看着 DOM 自动更新，看起来很有意思。你知道更有意思的是啥吗？给这些值补间。Svelte 提供了一些能帮助我们通过动画表达变动，以构建丝滑 UI 的工具。

让我们先把 `progress` store 改成 `tweened` store：

```svelte
/// file: App.svelte
<script>
	import { +++tweened+++ } from 'svelte/+++motion+++';

	const progress = +++tweened+++(0);
</script>
```

现在点击按钮会让进度条产生过渡到新值的动画，但是效果稍微有点机械，不太令人满意。我们需要加一个缓动函数：

```svelte
/// file: App.svelte
<script>
	import { tweened } from 'svelte/motion';
	+++import { cubicOut } from 'svelte/easing';+++

	const progress = tweened(0, +++{
		duration: 400,
		easing: cubicOut
	}+++);
</script>
```

> `svelte/easing` 模块包含了 [Penner 缓动方程](https://web.archive.org/web/20190805215728/http://robertpenner.com/easing/)，或者你也可以提供自己的 `p => t` 函数，其中 `p` 和 `t` 都是 0 到 1 之间的值。

`tweened` 的所有选项设置如下：

- `delay` — 补间开始前的微秒数
- `duration` — 要么是一个微妙单位的补间持续时间，要么是一个 `(from, to) => milliseconds` 函数，以便为更大幅度的值的变化指定更长的补间
- `easing` — 一个 `p => t` 函数
- `interpolate` — 一个自定义的 `(from, to) => t => value` 函数，用以在任意值之间插值。默认情况下，Svelte 只会在数字、日期和相同结构的数组与对象（只要它们只包含数字和日期，或者其他合法的数组和对象）之间插值。如果你想给其他数据插值，比如表示颜色的字符串，或者变换矩阵等，你需要提供一个自定义的插值函数

你也可以给 `progress.set` 和 `progress.update` 传递这些选项，作为第二个参数，以覆盖默认选项。`set` 和 `update` 两个函数都会返回一个 promise，在补间完成后产生结果（resolve）。
