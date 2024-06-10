---
title: SvelteKit 是什么？
---

Svelte 是一个 _组件框架_，而 SvelteKit 是一个 _应用框架_（或者叫“元框架”，取决于你问谁）。SvelteKit 旨在解决构建生产环境应用时会遇到的那些棘手的问题：

- 路由
- 服务端渲染
- 数据抓取
- Service workers
- TypeScript 集成
- 预渲染
- 单页应用（SPA）
- 库打包
- 生产构建优化
- 部署到不同的托管提供商
- ……等等等等

SvelteKit 应用默认是服务端渲染的（就跟传统的多页应用（MPA）一样），以达到优秀的首次加载性能和 SEO 特性。但是后期也可以转到客户端导航（就跟现代的单页应用（SPA）一样），以避免用户每次导航时都要加载所有内容（包括像第三方分析代码之类的东西）。只要是 JavaScript 可以运行的地方，SvelteKit 应用都可以运行，甚至，你的用户完全用不着运行 JavaScript，你会见到的。

如果这听起来有点复杂，不用担心，SvelteKit 是一个可以伴你成长的框架！先从简单的地方开始，等到你需要的时候，再学习新特性。

## 项目结构

在右侧，树状的文件预览界面，你会看到一个项目中 SvelteKit 所需要的一堆文件。

`package.json` 对你来说应该会很熟悉，如果你之前用过 Node.js。这个文件列举了项目的依赖，包括 `svelte` 和 `@sveltejs/kit`，还有一些 `scripts` 用来与 SvelteKit CLI 交互。（我们现在就正在下面的窗口中运行 `npm run dev`）

> 注意文件中指定了 `"type": "module"`，这意味着 `.js` 文件会被默认当作一个原生的 JavaScript 模块，而不是传统的 CommonJS 格式。

`svelte.config.js` 包含了项目的配置。我们现在不需要关注这个文件，但如果你很好奇的话，可以访问 [这个文档](https://kit.svelte.dev/docs/configuration)。

`vite.config.js` 包含了 [Vite](https://vitejs.dev/) 的配置。因为 SvelteKit 使用 Vite。你可以使用诸如热模块更换、TypeScript 支持、静态资源处理等 [Vite 特性](https://vitejs.dev/guide/features.html)。

`src` 是存储应用源代码的地方。`src/app.html` 是页面模板（SvelteKit 会适当地替换 `%sveltekit.head%` 和 `%sveltekit.body%`），`src/routes` 定义了应用的 [路由](/tutorial/pages)。

最后，`static` 包含了所有的资源文件（比如 `favicon.png` 或者 `robots.txt`），可以包含在应用的部署中。