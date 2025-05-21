<script setup>
import MarkdownSlides from './components/MarkdownSlides.vue';
import { ref } from 'vue';

const markdownContent = ref(`
# Reveal.js 示例

一个用 Vue 和 Reveal.js 创建的 Markdown 幻灯片演示。

---

<!-- .slide: data-background="#2A2A2A" -->
## 通过碎片播放多个音频

* 第一个音频 (播放完自动下一个) <!-- .element: class="fragment" data-fragment-index="1" data-audio-src="/audio/test.mp3" data-audio-loop="false" -->
* 第二个音频 (循环播放，延迟后下一个) <!-- .element: class="fragment" data-fragment-index="2" data-audio-src="/audio/test.mp3" data-audio-loop="false" -->
* 第三个音频 (播放完自动下一个) <!-- .element: class="fragment" data-fragment-index="3" data-audio-src="/audio/test.mp3" data-audio-volume="0.3" data-audio-loop="false" -->


---

## 数学公式 (Math Plugin)

使用 KaTeX 渲染:

行内公式: $E = mc^2$

块级公式:
$$
\\frac{\\partial \\rho}{\\partial t} + \\nabla \\cdot (\\rho \\mathbf{v}) = 0
$$

---

## 基本功能

*   支持 Markdown
*   水平和垂直幻灯片
*   代码高亮

--

### 垂直幻灯片

按向下箭头查看。

---

<!-- .slide: data-background="#f7f7f7" -->
## 布局示例

<div style="display: flex; width: 100%;">
<div style="flex: 1; text-align: left; padding-right: 20px;">

### 左侧内容

这是左边栏。

*   要点 1
*   要点 2

</div>
<div style="flex: 1; text-align: left;">

### 右侧内容

这是右边栏。

<img src="https://vuejs.org/images/logo.png" width="200" />

</div>
</div>

---

## 动画 (Fragments)

*   第一个项目 <!-- .element: class="fragment" data-audio-src="assets/test.mp3" -->
*   第二个项目 <!-- .element: class="fragment fade-up" -->
*   第三个项目 <!-- .element: class="fragment grow" -->

`);

// Reveal.js 配置选项示例
const revealOptions = ref({
  transition: 'slide', // 切换效果
  // 可以添加更多 reveal.js 配置项
});

</script>

<template>
  <div >
    <MarkdownSlides
        :markdown-content="markdownContent"
        :reveal-options="revealOptions"
    />
    <!-- 你可以在这里添加一个文本域来编辑 Markdown -->
    <textarea v-model="markdownContent" style="width: 100%; height: 200px;"></textarea>
  </div>
</template>

<style>

</style>
