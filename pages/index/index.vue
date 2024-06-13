<script setup lang="ts">
import type { videoItem } from '@/types/video'
useHead({
  meta: [
    {
      name: 'referrer',
      content: 'no-referrer'
    }
  ]
})
//
const { data: channelList } = await useFetch('/api/channel')
const { data: videolList } = await useFetch('/api/video')

// 用于列表
const list = ref<videoItem[]>([]);
// 加载状态
const loading = ref(false);
// 是否加载完成
const finished = ref(false);


// yema 
let page = 1
let pageSize = 20
// 滚动触底触发
const onLoad = () => {
  loading.value = false
  //根据当前页面进行提取数据
  const data = videolList.value?.slice((page - 1) * pageSize, page * pageSize) as videoItem[]
  list.value.push(...data)
  page++
  if (videolList.value?.length === list.value.length) {
    finished.value = true
  }
}

// 初始化加载-主动请求20条数据,用于首屏渲染,方便seo 抓取到数据
onLoad()

</script>

<template>
  <AppHeader />
  <!-- 频道模块 -->
  <van-tabs>
    <van-tab v-for="item in channelList" :key="item.id" :title="item.name" />
  </van-tabs>
  <!-- 视频列表 -->
  <van-list v-model:loading="loading" :finished="finished" finished-text="没有更多了" @load="onLoad">
    <!-- <van-cell v-for="item in list" :key="item" :title="item" /> -->

    <div class="video-list">
      <AppVideo v-for="item in list" :key="item.bvid" :item="item" />
    </div>
  </van-list>
</template>

<style lang="scss">

// 视频列表
.video-list {
  display: flex;
  flex-wrap: wrap;
  padding: 10px 5px;
}


</style>