---
title: css 动画
date: 2016-10-03 15:19:59
tags: css
---

animate动画
---

* `animation-name`动画的名字
* `animation-duration` 动画持续的时间
* `animation-timing-function` 为动画的曲线
	* linear	动画从头到尾的速度是相同的。
	* ease	默认。动画以低速开始，然后加快，在结束前变慢。
	* ease-in	动画以低速开始
	* ease-out	动画以低速结束
	* ease-in-out	动画以低速开始和结束
	* cubic-bezier(n,n,n,n) 在 cubic-bezier 函数中自己的值。可能的值是从 0 到 1 的数值。
* `animation-delay` 规定在动画开始之前的延迟
* `animation-iteration-count` 动画播放的次数
* `animation-direction` 属性定义是否应该轮流反向播放动画
	* normal 动画正常播放
	* alternate 动画轮流反向播放
* `animation-fill-mode` 属性规定动画在播放之前或之后，其动画效果是否可见
	* none 不改变
	* forwards 动画完成后，保持最后一帧
	* backwards 动画完成后，保持第一帧
	* both 前后叠加效果
* `animation-play-state` 动画是暂停还是继续进行
	* 可以在js中进行操作 `object.style.animationPlayState="paused"`

<style>
.box {
	width: 100px;
	height: 100px;
	background-color: red;
	-webkit-animation: move 2s; // 动画持续的时间
  animation-timing-function: ease-in-out; // 动画的表现方式
  -webkit-animation-timing-function: ease-in-out;
  animation-iteration-count: 20;
  animation-direction: alternate;
}

@keyframes move {
  0% {
    transform: translateX(0rem);
  }
  100% {
    transform: translateX(3rem);
    opacity: 0;
  }
}
</style>


```css
.box {
	width: 100px;
	height: 100px;
	background-color: red;
	animation-name: move; // 动画名字
	animation-duration: 2000ms; // 动画持续时间
  	animation-timing-function: ease-in-out; // 动画的表现方式
  	animation-iteration-count: 20; // 持续次数
  	animation-direction: alternate; // 轮播方式
}

@keyframes move {
  0% {
    transform: translateX(0rem);
  }
  100% {
    transform: translateX(3rem);
    opacity: 0;
  }
}

```


transform动画
---

#### transition属性

* transition-property	规定设置过渡效果的 CSS 属性的名称。
* transition-duration	规定完成过渡效果需要多少秒或毫秒。
* transition-timing-function	规定速度效果的速度曲线。
* transition-delay	定义过渡效果何时开始。

#### transform属性

* none	定义不进行转换。
* matrix(n,n,n,n,n,n)	定义 2D 转换，使用六个值的矩阵。
* matrix3d(n,n,n,n,n,n,n,n,n,n,n,n,n,n,n,n)	定义 3D 转换，使用 16 个值的 4x4 矩阵
* translate(x,y)	定义 2D 转换。
* translate3d(x,y,z)	定义 3D 转换。
* translateX(x)	定义转换，只是用 X 轴的值。
* translateY(y)	定义转换，只是用 Y 轴的值。
* translateZ(z)	定义 3D 转换，只是用 Z 轴的值。
* scale(x,y)	定义 2D 缩放转换。
* scale3d(x,y,z)	定义 3D 缩放转换。
* scaleX(x)	通过设置 X 轴的值来定义缩放转换。
* scaleY(y)	通过设置 Y 轴的值来定义缩放转换。
* scaleZ(z)	通过设置 Z 轴的值来定义 3D 缩放转换。
* rotate(angle)	定义 2D 旋转，在参数中规定角度。
* rotate3d(x,y,z,angle)	定义 3D 旋转。
* rotateX(angle)	定义沿着 X 轴的 3D 旋转。
* rotateY(angle)	定义沿着 Y 轴的 3D 旋转。
* rotateZ(angle)	定义沿着 Z 轴的 3D 旋转。
* skew(x-angle,y-angle)	定义沿着 X 和 Y 轴的 2D 倾斜转换。
* skewX(angle)	定义沿着 X 轴的 2D 倾斜转换。
* skewY(angle)	定义沿着 Y 轴的 2D 倾斜转换。
* perspective(n)	为 3D 转换元素定义透视视图。

例子

<style>
#box {
  width: 100px;
  height: 100px;
  background-color: red;
  transition-duration: 1s;
}
#box:hover {
	transform:scale(1.2);
}
</style>
<div id="box"></div>

```css
#box {
  width: 100px;
  height: 100px;
  background-color: red;
  transition-duration: 1s; // 动画持续时间
}
#box:hover {
	transform:scaleX(1.2);
}
```

如果设置了transform的变化 都是会脱离文档流
