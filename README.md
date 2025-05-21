该markdown组件致力于将md转换为视频
Reveal.js-Vue 集成组件使用笔记

📝 Markdown 语法规范

1. 基础结构
```markdown
<!-- 主幻灯片 -->
# 主标题

副标题通过空行分隔

---

<!-- 第二张水平幻灯片 -->
## 水平分页
使用三个换行加 `---` 分隔

--

<!-- 垂直子页 -->
## 垂直分页
用三个换行加 `--` 分隔

--

<!-- 第二个垂直子页 -->
## 第二子页
```

2. 片段功能
```markdown
- 默认片段 ::: fragment
- 渐现片段 ::: fragment fade-in
- 高亮片段 ::: fragment highlight-red

<!-- 带音频的片段 -->
<li class="fragment" data-audio-src="/sound/effect.mp3">播放音效</li>
```

3. 数学公式
```markdown
行内公式 $E=mc^2$

块级公式：
$$
\begin{aligned}
  \nabla \cdot \mathbf{E} &= \frac {\rho} {\varepsilon_0} \\
  \nabla \cdot \mathbf{B} &= 0
\end{aligned}
$$
```

4. 代码演示
````markdown
```javascript [示例]
function greet(name) {
  console.log(`Hello ${name}!`)
}
greet("Reveal.js")
```

```python [动画片段]
带渐变动画的代码
def factorial(n):
    return 1 if n == 0 else n * factorial(n-1)
```
````

5. 多媒体集成
```markdown
<!-- 背景音频 -->
<section data-background-audio="/music/bgm.mp3">

<!-- 视频嵌入 -->
<video data-autoplay src="/video/demo.mp4"></video>
```

⚙️ 使用配置

初始化参数
```js
// 组件 props 配置
separator: '^\\r?\\n---\\r?\\n'  // 水平分隔正则
verticalSeparator: '^\\r?\\n--\\r?\\n' // 垂直分隔正则
autoSlide: 5000 // 自动播放间隔
```

音频管理
```markdown
<!-- 音频控制快捷键 -->
暂停/恢复: S键
音量增/减: ↑/↓键
```

💡 最佳实践

1. 目录结构建议：
```
public/
  ├── audio/
  │    └── effect.mp3
  └── slides/
       └── presentation.md
```

2. 路径处理：
```markdown
<!-- 使用绝对路径引用 -->
data-audio-src="/audio/transition.wav"
```

3. 动画时序：
```markdown
<!-- 带延迟的片段 -->
<li class="fragment" data-fragment-index="2" 
    data-audio-src="/sound/ding.mp3">第二步</li>
```

⚠️ 注意事项

1. 音频自动播放限制：
   • 需在用户交互后触发（如点击导航按钮）


2. 移动端适配：
   ```css
   /* 添加响应式 meta 标签 */
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```

3. 打印优化：
   ```js
   // 添加 PDF 导出配置
   Reveal.configure({ pdfSeparateFragments: false });
   ```
