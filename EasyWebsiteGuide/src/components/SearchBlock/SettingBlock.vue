//搜索引擎设置组件
<template>
  <div class="setting">
    <img
      src="@/assets/X.svg"
      height="20px"
      class="icon_X"
      width="20px"
      @click="this.changeSettingBlockShow"
    >
    <br /><span class="text">添加搜索引擎</span>
    <Engines
      v-for="engine in this.engineMap"
      :key="engine.name"
      :engineName="engine.name"
      :isEngineShow="engine.isEngineShow"
    />
    <input
      type="button"
      class="addButton"
      @click="this.changeEngineShowMap"
      value="Add"
    >
  </div>
</template>

<script>
//单个的可供选择的搜索引擎
import Engines from "@/components/SearchBlock/Engines.vue"

export default {
  name: "SettingBlock",
  components: {
    Engines
  },
  props: [
    //function:更改显示的搜索引擎
    'changeEngineShowMap',
    //function:更改搜索引擎设置的显示
    'changeSettingBlockShow',
    //可供选择的搜索引擎表
    'engineMap'
  ],
};
</script> 

<style>
.setting {
  position: absolute;
  right: 0;
  margin-right: 30px;
  height: 100%;
  width: 200px;
  border-radius: 30px;
  text-align: left;
  background-color: rgba(244, 244, 244, 0.1);
  backdrop-filter: blur(5px);
  box-shadow: 0 10px 10px 5px rgba(1, 1, 1, 0.4);
  animation: slide-in-blurred-right 0.6s cubic-bezier(0.23, 1, 0.32, 1) both;
}

.text {
  margin: 50px 0 0 30px;
  color: #f4f4f4;
  font-family: 黑体;
  font-size: 20px;
}

.addButton {
  height: 30px;
  width: 70px;
  border-style: none;
  margin-top: 50px;
  margin-left: 50px;
  opacity: 0.7;
  border-radius: 150px;
  background-color: #2f3640;
  color: #f4f4f4;
  font-size: 10px;
  transition-duration: 0.5s;
  animation: slide-in-blurred-top 0.6s cubic-bezier(0.23, 1, 0.32, 1) both;
}
@keyframes slide-in-blurred-top {
  0% {
    transform: translateY(-50px) scaleY(2.5) scaleX(0.2);
    transform-origin: 50% 0%;
    filter: blur(40px);
    opacity: 0;
  }
  100% {
    transform: translateY(0) scaleY(1) scaleX(1);
    transform-origin: 50% 50%;
    filter: blur(0);
    opacity: 0.7;
  }
}
.addButton:hover {
  box-shadow: 0 10px 20px 0px rgba(1, 1, 1);
  opacity: 0.95;
}
.icon_X {
  position: absolute;
  right: 15px;
  top: 10px;
  transition: 0.5s;
}
.icon_X:hover {
  background: #000;
  opacity: 0.5;
  border-radius: 5px;
}
</style>