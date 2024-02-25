## 选择器优先级 样式优先级

- !important

- 行内样式

- ID选择器

- 伪类选择器 `:hover`

- Class选择器

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

## BFC规范

## 清除浮动的方式

## 双飞翼&&圣杯布局实现

- 圣杯：两侧宽度固定，中间自适应，中间一栏先加载渲染 （float + margin）

## css哪些属性可以继承

- 字体的属性 `font`

- 文本的属性 `line-height`

- 元素的可见性 `visibility:hidden`

- 表格布局的属性 `border-spacing`

- 列表的属性 `list-style`

- 页面的样式属性 `page`

- 声音的样式属性

## 处理文本超出长度问题

## Flex布局

## Grid布局
