<template>
  <div id="app">
    <!-- 显示当前路由对应的视图组件 -->
    <router-view></router-view>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
// 引入背景音乐文件
import bgm from './assets/audios/bgm.mp3';

// 创建音频对象
const audio = ref(new Audio(bgm));

onMounted(() => {
  // 设置循环播放
  audio.value.loop = true;
  // 播放音乐
  audio.value.play().catch((error) => {
    console.warn('自动播放音乐失败，用户需先与页面交互', error);
  });
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
