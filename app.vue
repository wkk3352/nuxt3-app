<template>

  <!-- Nuxt是基于文件路由系统  -->
  <!--NuxtPage 相当于routerview  -->
  <!-- keepalive 缓存页面 -->
  <NuxtPage :keepalive="{max: 10}" />


</template>
<script setup lang="ts">
useSeoMeta({
  // 网站标题
  title: '哔哔哩标题',

  // 网站描述
  description: '这是哔哔',
  // 搜索关键字
  keywords: '搜索关键字'
})

</script>
<style lang="scss">
// 基础样式
@import './assets/styles/base.scss';
// 字体图标
@import './assets/styles/iconfont.scss';
</style>
<style>
:root {
  /* css  变量设置组件库主题 */
  --van-primary-color: #fb7299;
}
</style>