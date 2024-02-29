## CSS 3 新特性

- 圆角（border-radius）：允许你给元素添加圆角，而无需使用图片或其他复杂的方法。

- 阴影（box-shadow 和 text-shadow）：可以给元素或文字添加阴影效果，提升视觉效果。

- 渐变（linear-gradient 和 radial-gradient）：允许你为元素背景设置颜色渐变，增加了设计上的多样性。

- 过渡（transition）：允许你为属性变化设置动画效果，使状态变化更加平滑。

- 动画（@keyframes 和 animation）：允许你创建复杂的动画序列，而无需依赖JavaScript。

- 变形（transform）：允许你对元素进行旋转、缩放、倾斜或平移。

- 弹性盒模型（flexbox）：为布局提供了一种更加灵活和强大的方式，特别是在响应式设计中。

- 网格布局（grid）：提供了一种基于网格的布局系统，使复杂布局的实现变得更加简单。

- 多媒体查询：允许你根据不同的屏幕大小或设备特性应用不同的样式规则，是响应式设计的关键。

- 自定义属性（CSS变量）：允许你定义可以在整个文档中重复使用的变量，简化了样式表的维护。

- 滤镜（filter）：提供了一系列图像处理效果，如模糊、对比度调整等。

- 混合模式（mix-blend-mode）：允许元素与其背景以不同的方式混合。

- 形状（shape-outside）：允许你围绕非矩形形状进行文本布局。

- 计算函数（calc()）：允许你在CSS中进行简单的计算。

- 媒体查询：改进了响应式设计的支持，使得针对不同设备和条件应用不同的样式更加方便。

## 选择器优先级 样式优先级

- !important

- 行内样式

- ID 选择器

- 伪类选择器 `:hover`

- Class 选择器

- 属性选择器 `[name=xxx]`

- 标签选择器

- 全局选择器

## 水平垂直居中的方法

- 定位 + margin
  
  ```css
  .father {
    position: relative;
  }
  
  .son {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
  }
  ```

- 定位 + transform
  
  ```css
  .father {
    position: relative;
  }
  
  .son {
    position: absolute;
    transform: translate(-50%, -50%);
  }
  ```

- flex 布局
  
  ```css
  .father {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  ```

- grid 布局

- table 布局

## BFC 规范

**区块格式化上下文**（Block Formatting Context，BFC）是 Web 页面的可视 CSS 渲染的一部分，是块级盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。BFC 的子元素不会对外面的元素产生影响

### 创建 BFC

- 文档根元素 `<html>`

- 浮动元素

- 绝对定位元素 `position:absolute/fixed`

- 行内块元素 `display:inline-block`

- 表格单元格/标题 `display:table-cell/table-caption`

- `overflow` 值不为  `visible`  或  `clip`  的块级元素

- `display`  值为  `flow-root`  的元素

- `contain`  值为  `layout`、`content`  或  `paint`  的元素
* 弹性元素 `display`值为  `flex`  或  `inline-flex`

* 网格元素 `display`值为  `grid`  或  `inline-grid`

* 多列容器（[`column-count`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/column-count)  或  [`column-width` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/column-width "Currently only available in English (US)")  值不为  `auto`，且含有  `column-count: 1`  的元素）。

* `column-span`  值为  `all`  的元素始终会创建一个新的格式化上下文，即使该元素没有包裹在一个多列容器中（[规范变更](https://github.com/w3c/csswg-drafts/commit/a8634b96900279916bd6c505fda88dda71d8ec51)、[Chrome bug](https://bugs.chromium.org/p/chromium/issues/detail?id=709362)）

### BFC 解决什么问题

- `margin` 重合问题

- `margin` 塌陷问题

- 高度坍塌问题

## 清除浮动的方式

- 在最后一个浮动标签后添加标签，样式为 `clear:both`

- 父元素添加 `overflow:hidden` 触发 BFC 方式

- 使用 `after` 伪元素，IE6/7 不支持，应使用 `zoom:1`

## 双飞翼&&圣杯布局实现

- 两侧宽度固定，中间自适应，中间一栏先加载渲染 （float + margin）

## css 哪些属性可以继承

- 字体的属性 `font`

- 文本的属性 `line-height`

- 元素的可见性 `visibility:hidden`

- 表格布局的属性 `border-spacing`

- 列表的属性 `list-style`

- 页面的样式属性 `page`

- 声音的样式属性

## 处理文本超出长度问题

- 单行文本 `text-overflow: ellipsis` 
  
  ```css
  .text-overflow {
   white-space: nowrap; /* 确保文本在一行内显示 */
   overflow: hidden; /* 隐藏超出部分 */
   text-overflow: ellipsis; /* 显示省略号 */
  }
  ```

- 多行文本
  
  ```css
  .multi-line-ellipsis {
   display: -webkit-box;
   -webkit-box-orient: vertical;
   -webkit-line-clamp: 3; /* 限制为3行 */
   overflow: hidden;
  }
  ```

## Flex 布局

## Grid 布局

## 动画原理

## 浏览器兼容

## 背景平铺


