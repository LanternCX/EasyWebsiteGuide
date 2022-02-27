<template>
  <input
    type="button"
    class="engineSwitch"
    ref="engineSwitch"
    :id="this.engineName"
    :value="this.engineName"
    @click="changeSearchEngineAndStyle(engineName)"
    :style="btnStyle"
  >

</template>

<script>
export default {
  name: 'EngineSwitch',
  props: [
    'engineName',
    'changeSearchEngine'
  ],
  data() {
    return {
      btnStyle: '',
    };
  },
  mounted() {
    this.$bus.$on('btnStyle')
  },
  methods: {
    changeSearchEngineAndStyle(engineName) {
      this.changeSearchEngine(engineName)
    }
  }
}
</script>

<style>
.engineSwitch {
  height: 30px;
  width: 70px;
  border-style: none;
  margin-top: 5px;
  margin-right: 5px;
  opacity: 0.7;
  border-radius: 150px;
  background-color: #2f3640;
  color: #f4f4f4;
  transition-duration: 0.5s;
  animation: slide-in-blurred-top-2 0.6s cubic-bezier(0.23, 1, 0.32, 1) both;
}
.engineSwitch:hover {
  box-shadow: 0 10px 20px 0px rgba(1, 1, 1);
  opacity: 0.95;
}
.engineSwitch:active {
  background-color: #7f8c8d;
}
@keyframes slide-in-blurred-top-2 {
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
</style>