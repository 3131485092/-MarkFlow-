<template>
  <div class="reveal">
    <div class="slides">
      <section data-markdown :data-separator="separator" :data-separator-vertical="verticalSeparator">
        <textarea data-template>
          {{ markdownContent }}
        </textarea>
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import Reveal from 'reveal.js';
import Markdown from 'reveal.js/plugin/markdown/markdown.esm.js';
import MathPlugin from 'reveal.js/plugin/math/math.esm.js';
import 'reveal.js/dist/reveal.css';
import 'reveal.js/dist/theme/black.css';

const revealInstance = ref(null);
const audioElements = ref({}); // 存储音频元素
const currentAudio = ref(null); // 追踪当前正在播放的音频

const props = defineProps({
  markdownContent: String,
  separator: {type: String, default: '^\r?\n---\r?\n'},
  verticalSeparator: {type: String, default: '^\r?\n--\r?\n'}
});

const initializeReveal = async () => {
  const revealEl = document.querySelector('.reveal');
  if (!revealEl) return;

  revealInstance.value = new Reveal(revealEl, {
    plugins: [Markdown, MathPlugin],
    hash: true,
    slideNumber: true,
    autoSlide: 5000,
    autoSlideStoppable: true,
  });

  try {
    await revealInstance.value.initialize();
    // 设置片段音频支持
    setupFragmentAudio();
  } catch (error) {
    console.error('Failed to initialize reveal.js:', error);
  }
};

const setupFragmentAudio = () => {
  if (!revealInstance.value) return;

  // 处理片段显示事件
  revealInstance.value.on('fragmentshown', async (event) => {
    const fragment = event.fragment;
    const audioSrc = fragment.getAttribute('data-audio-src');

    if (audioSrc) {
      // 创建或重用音频元素
      const audio = new Audio(audioSrc);
      audio.preload = 'auto';
      audioElements.value[audioSrc] = audio;
      try {
        await audioElements.value[audioSrc].play();
        currentAudio.value = audioElements.value[audioSrc];
      } catch (error) {
        console.error('音频播放失败:', error);
      }
    }
  });
};

onMounted(() => {
  initializeReveal();
});

onBeforeUnmount(() => {
  // 清理音频元素
  Object.values(audioElements.value).forEach(audio => {
    audio.pause();
    audio.currentTime = 0;
  });

  if (revealInstance.value) {
    revealInstance.value.destroy();
    revealInstance.value = null;
  }
});
</script>

<style scoped>
.reveal {
  height: 100vh;
}
</style>