<template>
  <div>
    <router-view />
  </div>
</template>

<style>
#app {
  padding: 60px;
  max-width: 1024px;
  margin: 0 auto;
  background: url("./assets/background.jpg") rgba(255, 255, 255, 0.1); /* 添加一个白色背景，透明度为 0.8 */
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* 添加一些阴影 */
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
