<template>
    <div>
        <AppHeader />
        <h2>视频页{{$route.params.id}}</h2>
    </div>
</template>

<script lang="ts" setup>
const { params } = useRoute()
console.log(params);


</script>

<style scoped></style>