//单个的可供选择的搜索引擎组件
<template>
  <div class="engines">
    <input
      type="checkbox"
      id="checkbox"
      :checked="isEngineShow"
      @click="changeShow"
    ><span> {{ engineName }} </span>
  </div>

</template>

<script>
export default {
  name: "Engines",
  props: ['engineName', 'isEngineShow'],
  methods: {
    //组件间通信：使用全局事件总线
    //发送这个搜索引擎的名字到SearchBlock
    changeShow() {
      this.$bus.$emit('engineName', this.engineName)
    }
  }
}
</script>

<style>
.engines {
  margin: 10px 0 0 50px;
  color: #f4f4f4;
}
.checkbox {
  border-style: none;
  transition: 1s;
}
.checkbox:checked {
  background-color: black;
  border-style: none;
}
</style>