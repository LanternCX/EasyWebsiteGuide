<template>
  <div id="app">
    <guide-block></guide-block>
    <search-block></search-block>
  </div>
</template>

<script>
//搜索框模块
import SearchBlock from '@/components/SearchBlock/SearchBlock.vue'
//书签框模块
import GuideBlock from '@/components/GuideBlock/GuideBlock.vue'

export default {
  name: 'App',
  components: {
    SearchBlock,
    GuideBlock
  }
}

</script>

<style>
#app {
  width: 100%;
  min-width: 550px;
  height: 100%;
  min-height: 540px;
  background: url("./assets/bg.png") no-repeat;
  background-size: cover;
  text-align: center;
  color: #2c3e50;
  overflow: hidden;
}
</style>
