---
title: css注意与问题
type: cookbook
order: 6
---

`text-overflow`实际上是作用在`text`标签的，我们需要为`text`标签设置宽度，以及把该属性设置在`text`标签上面，而不是在他的父组件上面.

单行省略：

```css
.ellipsis {
	width: 100rpx;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap; /* no-app-nvue */
	lines: 1; /* app-nvue */
}
```

多行省略：

app-nvue

```css
.ellipsis {
	width: 100rpx;
	overflow: hidden;
	text-overflow: ellipsis;
	lines: 2; /* app-nvue */
}
```

no-app-nvue

```css
.ellipsis {
	width: 100rpx;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	-webkit-line-clamp: 2;
	overflow: hidden;
}
```
