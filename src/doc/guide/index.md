---
title: 快速上手
type: guide
order: 2
---

mypUI 是基于 uniapp 的一套组件库与工具集，可以 **高效且规范** 地开发出 uniapp 支持的各端应用（APP/各家小程序/H5/快应用）。兼容 nvue 页面 和 vue 页面。nvue 页面对应的 app端 依托 weex 编译为原生，具备良好的性能与体验。mypUI 绝对能为您带来 **稳定、高效、规范** 的开发体验。

## 集成mypUI

### 拷贝UI组件

直接将`mypUI`放在您的项目根目录下。

### 复制UI的静态资源

`loadingSrc`等公用静态资源直接使用了示范UI项目中 `/static/ui` 下面的静态文件，没有使用网络图片，所以需要拷贝到自己的项目下（`/static/ui`这个路径还是需要保持一致的）。

静态文件的路径依然保持和示范项目中一致即可也就是依然是 `/static/ui` 路径。

### 使css生效

为了减少包体积，UI内使用了 `全局css` 。您需要在 `app.vue` 里面引入 `mypUI` 中的 `base.scss`。

也就是：

``` html
<style lang="scss">
	@import '@/mypUI/base.scss';
</style>
```

因为使用了 `scss变量`，记得设置 `style` 的 `lang="scss"`。

### 配置 `easycom`

UI内部使用了 `easycom` 的组件自动引入，所以您必须在项目中开启 `easycom`。

在 `pages.json` 中添加如下代码：

```js
"easycom": {
	"autoscan": true,
	"custom": {
		"myp-(.*)": "@/mypUI/myp-$1/myp-$1.vue" // 匹配mypUI内的vue文件
	}
}
```

> easycom 是什么？请看官方文档 [easycom](https://uniapp.dcloud.io/collocation/pages?id=easycom)

### 定义您的 UI 主题

`mypUI` 下的 `mypui.scss` 是主题 `scss变量` 定义文件。您需要根据您的项目UI的主题色对其进行修改。

如果主题内定义的变量无法满足您的要求，您可以在里面进行添加，并适当在 `base.scss` 里面增加相应的 `class` 即可。

关于主题的具体说明与使用，请查阅 [主题](/doc/guide/theme.html)。

如果您需要用到主题内定义的`scss变量`，一定要记得在使用的地方引入`mypui.scss`，否则编译会报错。

```html
<style lang="scss">
	@import '@/mypUI/mypui.scss';
</style>
```

<p class="tip">注意：在 app.vue 里面全局引入 mypui.scss 是不会起作用的。毕竟里面只是定义了一些 scss变量</p>

### 初始化系统变量

我们建议您在 `onLaunch` 里面对系统变量进行初始化（当然，这是可选的，`mypUI` 内部接口会根据需要调用初始化的接口）。

初始化代码如下：

- 先引入并放入mixins；

- 然后调用初始化方法；

```html
<script>
	import systemMixin from '@/mypUI/myp-mixin/systemMixin.js'
	
	export default {
		globalData: {
			currentTab: 0
		},
		mixins: [systemMixin],
		onLaunch: function() {
			console.log('App Launch')
			// #ifdef APP-NVUE || H5
			this.mypInitSystemInfo()
			// #endif
			// #ifndef APP-NVUE || H5
			setTimeout(()=>{
				this.mypInitSystemInfo()
			}, 0)
			// #endif
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	@import '@/mypUI/base.scss';
</style>
```

### 现在开始愉快的使用吧

自由且无需手动导入 `mypUI` 的使用方式，正式开始。

祝您使用愉快。

<p class="tip">如果在使用的过程中，您发现有任何不如意或者bug存在，敬请联系我们，或者给出您的宝贵意见。当然，您也可以给出您的实现方式。或者给我们提一个 <a href="https://github.com/wakaryry/mypUI">pr</a></p>

## 找到代码与我们

- [mypUI-github](https://github.com/wakaryry/mypUI) 欢迎star

- [mypUI-uniapp插件市场](https://ext.dcloud.net.cn/plugin?id=2190) 需要您的好评

- [mypUI-文档开源](https://github.com/wakaryry/mypui-doc)

- [mypUI-文档地址](https://www.mypui.cn)

- 作者wx：`pptpdf`

- 作者qq：`382006503`

- 欢迎加入wx群和qq群。wx群请加wx，qq群请加qq群号：`306797275`

<p class="tip">强烈建议加入wx与qq群，获取更多mypUI的动态与帮助</p>

## 快速体验

- 安装HBuilderX；
- 下载或者clone本UI库；
- 在HBuilderX里面打开或者导入；
- 运行到自己想要体验的平台即可；

<p class="tip">想了解我们是怎么使用 mypUI 的吗？又如何对 mypUI 有一个更加全面的了解？或者说站在一个代码设计者的角度去了解 mypUI? 纵观全局，对你更加高效的使用mypUI非常有用。建议您一定要看看</p>

<a class="button" href="global.html">全局视角了解mypUI</a>

您可以配合 mypUI 的示范代码 来做更加深入的理解。
