<template>
  <div class="app-container">
    <PhaseShardGraph />
  </div>
</template>

<script setup lang="ts">
import PhaseShardGraph from './components/PhaseShardGraph.vue'
</script>

<style>
/* 核心重置与全局变量 */
:root {
  --vp-c-bg: #1e1e20;
  --vp-c-bg-soft: #252529;
  --vp-c-bg-alt: #161618;
  --vp-c-bg-mute: #2c2c30;
  --vp-c-border: #3c3f44;
  --vp-c-text-1: #ffffff;
  --vp-c-text-2: #ebebf5;
  --vp-c-text-3: #a1a1aa;
  --vp-c-brand-1: #00F0FF;
  /* 赛博青 */
  --vp-c-brand-2: #B026FF;
  /* 赛博紫 */
  --vp-font-family-base: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
  --vp-font-family-mono: ui-monospace, SFMono-Regular, "SF Mono", Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;
}

body,
html {
  margin: 0;
  padding: 0;
  width: 100vw;
  height: 100vh;
  background-color: var(--vp-c-bg);
  color: var(--vp-c-text-1);
  overflow: hidden;
  /* 防止全局滚动条 */
}

.app-container {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  /* 给组件留一点边距 */
  padding: 20px;
  box-sizing: border-box;
}
</style>