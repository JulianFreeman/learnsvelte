---
title: 自定义 CSS 过渡
---

`svelte/transition` 模块提供了很多内置的过渡函数，但是要创建自己的过渡函数也很容易。举例来说，下面是 `fade` 过渡的源码：

```js
/// no-file
function fade(node, { delay = 0, duration = 400 }) {
	const o = +getComputedStyle(node).opacity;

	return {
		delay,
		duration,
		css: (t) => `opacity: ${t * o}`
	};
}
```

这个函数接收两个参数：要应用过渡的节点，和其他任意要传入的参数；然后返回一个可以包含以下属性的过渡对象：

- `delay` — 过渡开始之前的微秒数
- `duration` — 以微妙为单位的过渡时长
- `easing` — 一个 `p => t` 缓动函数（详见 [补间](/tutorial/tweens)）
- `css` — 一个 `(t, u) => css` 函数，其中 `u === 1 - t`
- `tick` — 一个 `(t, u) => {...}` 函数，对节点有一些影响

`t` 的值在进入动画的开始和消失动画的结束为 `0`，在进入动画的结束和消失动画的开始为 `1`。

大部分时候你应该返回 `css` 属性而 _非_ `tick` 属性，因为 CSS 动画在主线程之外运行，以尽可能防止卡顿。Svelte 模拟了过渡并构建了一个 CSS 动画，然后运行它。

比如说，`fade` 过渡会生成一个类似下面这样的 CSS 动画：

```css
/// no-file
0% { opacity: 0 }
10% { opacity: 0.1 }
20% { opacity: 0.2 }
/* ... */
100% { opacity: 1 }
```

当然我们可以发挥更多创意。让我们做一些真正有意思的事情：

```svelte
/// file: App.svelte
<script>
	import { fade } from 'svelte/transition';
	+++import { elasticOut } from 'svelte/easing';+++

	let visible = true;

	function spin(node, { duration }) {
		return {
			duration,
			css: (t) => +++{
				const eased = elasticOut(t);

				return `
					transform: scale(${eased}) rotate(${eased * 1080}deg);
					color: hsl(
						${Math.trunc(t * 360)},
						${Math.min(100, 1000 * (1 - t))}%,
						${Math.min(50, 500 * (1 - t))}%
					);`;
			}+++
		};
	}
</script>
```

记住：能力越大，责任越大。
