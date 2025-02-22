---
title: '::-webkit-progress-bar'
slug: Web/CSS/::-webkit-progress-bar
tags:
  - CSS
  - 非标准特性
translation_of: Web/CSS/::-webkit-progress-bar
---
{{CSSRef}}{{Non-standard_header}}

## 概述

**`::-webkit-progress-bar`** [CSS](/en-US/docs/Web/CSS) [伪元素](/en-US/docs/Web/CSS/Pseudo-elements) 选择 {{HTMLElement("progress")}} 元素的未完成部分。 {{ cssxref("::-webkit-progress-value") }} 选择完成的部分。**`::-webkit-progress-bar`** 是{{cssxref("::-webkit-progress-inner-element")}} 伪元素的子元素，同时是 {{cssxref("::-webkit-progress-value")}} 伪元素的父元素。

> **备注：** 为了能让`::-webkit-progress-value`起作用，需要添加 CSS {{cssxref("-webkit-appearance")}} 至 `<progress>` 元素。

## 规范

没有规范。这是一个 WebKit/Blink 独有的规范。

## 例子

### CSS content

```css
progress {
  -webkit-appearance: none;
}

::-webkit-progress-bar {
   background-color: orange;
}
```

### HTML content

```html
<progress value="10" max="50">
```

### Output

{{EmbedLiveSample("Example", 200, 50)}}

应用了上述样式的进度条样式如下：

![](progress-bar.png)

## 浏览器兼容性

{{Compat("css.selectors.-webkit-progress-bar")}}

## 参见

- The pseudo-elements used by WebKit/Blink to style other parts of a {{HTMLElement("progress")}} element:

  - {{ cssxref("::-webkit-progress-value") }}
  - {{ cssxref("::-webkit-progress-inner-element") }}

- {{ cssxref("::-moz-progress-bar") }}
- {{ cssxref("::-ms-fill") }}
