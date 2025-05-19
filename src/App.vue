<template>
  <div id="app">
    <!-- 显示当前路由对应的视图组件 -->
    <router-view></router-view>
  </div>
</template>

<script setup>
// 这里可以添加全局的逻辑
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
