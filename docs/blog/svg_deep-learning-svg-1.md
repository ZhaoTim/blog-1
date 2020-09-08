SVG 全称 Scalable Vector Graphics (可缩放矢量图形)。它是一种用来描述二维矢量图形的 XML 标记语言。

本系列文章分为三个部分:

- 第一部分是 [SVG 基础](https://segmentfault.com/a/1190000015652209)。 主要讲 SVG 的一些基础知识，包括 SVG 基本元素，画布和视窗等。
- 第二部分是 [SVG 的坐标系统](https://segmentfault.com/a/1190000015661109)。主要会讲绘图坐标系， viewBox 以及preserveAspectRatio。
- 第三部分是 如何利用 SVG 来实现动画及交互。

> 最近写了一个 Sketch 插件，可以将 Sketch 图层压缩并转化为 React/React Native Component。欢迎到 GitHub 来 Star: https://github.com/reeli/sketch-svg-to-react-component

## SVG 基本元素及属性

### 渲染顺序
元素的渲染顺序非常重要，这决定了一个 SVG 中哪些元素可见，哪些元素不可见。SVG 元素的一个规则是**`“后来居上”`**，也就是说越后面的元素越可见。

```html
<svg width="100" height="100" style="outline: 2px solid red;">
	<rect x="0" y="0" width="50" height="50" fill="blue"/>
	<rect x="0" y="0" width="50" height="50" fill="green"/>
</svg>
```

![](../assets/svg-learning/svg-1.png)

> 在同一个位置创建了 50 * 50 的两个矩形，由于越后面的元素越可见，因此我们只能看到绿色的矩形，蓝色的矩形被它遮住了。

### SVG 值的单位
在 SVG 中，你可以指定值的单位，也可以不指定值的单位。如果不指定值的单位，则默认使用像素 (px) 作为单位。

```html
<svg width="100" height="100">
	<circle cx="0" cy="0" r="50%" fill="green">
</svg>
```
> width 和 height 都没有指定单位，那么它们的单位就是 px，相当于宽 100px 高 100px。`circle` 的 r 使用百分比作为单位，因为 100px*50%=50px，则圆的半径 r 等于 50px。

#### 单位列表
SVG 支持的长度单位包含了常见的 CSS 单位，如下:

| 单位  | 含义 |
| ------------- | ------------- |
| em | 相对于父元素的字体大小 |
| px | 相对于屏幕分辨率 |
| %  | 相对于父元素 |
| cm | 即厘米 |
| mm | 即毫米 |
| in | 即英寸 |
| pt | 1/72 英寸 |
| pc | 1/21 | 

## SVG 画布
SVG 画布就是用来绘制 SVG 内容的一个区域。这个画布可以无限延伸，你可以在这个画布的任何位置绘制你想要的内容。

## SVG 视窗（viewport）

SVG 视窗和浏览器视窗很像。你可以通过 SVG 视窗看到画布，但其实你只看到了画布的一部分，超过视窗的部分会被裁切并且隐藏。就像一个网页，它可能比浏览器的视窗宽，可能比浏览器的视窗长，但只有在视窗内的页面是可见的。

### 设置视窗大小

你可以通过给 `<svg>` 元素设置 `width` 和 `height` 来给 SVG 视窗设置宽和高。

当然，你也可以不给视窗设置宽和高，这就会交给用户代理程序去决定，一般默认是 300px * 150px。我们不推荐视窗使用默认的大小，最好还是根据自己的需求去定义。

```html
<!-- 视窗大小为 200px * 200px -->
<svg width="200" height="200">
	<circle cx="0" cy="0" r="100" fill="red"/>
</svg>
```

![](../assets/svg-learning/svg-2.png)

> 在 200px * 200px 的视窗内，以画布的 0,0 点(画布的原点和视窗的原点默认对齐)为圆心，半径为 100 画圆

### 为什么超过视窗的元素不可见

因为每个 SVG 元素都有一个默认的 `overflow: hidden` 样式，所以超过视窗的内容不可见。你也可以通过设置 `overflow: visible` 让超出视窗边界的内容变得可见。

```html
<svg width="100" height="100">
	<circle cx="0" cy="0" r="50" fill="green"/>
</svg>
```
![](../assets/svg-learning/svg-3.png)

## 深入理解画布和视窗

画布和视窗是两个容易混淆的概念，它们各自独立却又相互关联。理解清楚它们之间的关系很有必要。

为了更好的去理解这两个抽象概念，你可以把视窗想象成飞机上的窗户，把画布想象成无穷无尽的风景，只有在这个窗口内的风景才能被看到。 

![](../assets/svg-learning/viewport.jpg)

### 画布和视窗之间的关联

1. 每创建一个 `<svg>` 元素，就相当于创建了一个无穷大的画布，同时创建了一个视窗。
2. 画布和视窗分别对应两个坐标系统，一个用户坐标系，一个视窗坐标系，这两个坐标系统默认是对齐的。如果暂时不理解坐标系统也没关系，请继续往下看，我会在下一节详细说明。

点这里进入下一章 [SVG 的坐标系统](https://segmentfault.com/a/1190000015661109)


  [1]: /img/bVbdP2S
  [2]: /img/bVbdP4m
  [3]: /img/bVbdP4n
