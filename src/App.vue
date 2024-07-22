<template>
  <div>
    <router-view />
  </div>
</template>

<style>
body {
  background-image: url("./assets/background.jpg"); /* 替换为你的背景图片路径 */
  background-size: 1024px 1024px;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh;
  margin: 0;
}

#app {
  padding: 60px;
  max-width: 1024px;
  margin: 0 auto;
  background: rgba(255, 255, 255, 0.8); /* 添加一个白色背景，透明度为 0.8 */
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 添加一些阴影 */
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
<script setup lang="ts"></script>
