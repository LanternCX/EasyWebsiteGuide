// 搜索框组件 默认百度搜索
<template>
  <div>
    <div id="search">
      <span class="searchEngineURL"> SearchEngineURL: {{searchEngineURL}}</span>
      <div id="form">
        <input
          type="text"
          name="wd"
          placeholder="在此进行搜索..."
          class="searchInput"
          autocomplete="off"
          v-model="wd"
          @keypress.enter="search()"
        />
        <span
          class="searchBtn"
          @click="search()"
        >
          <img
            type="submit"
            src="@/assets/search.svg"
            width="30px"
            height="30px"
            class="icon"
          />
        </span>
      </div>

      <EngineSwitch
        v-for='engine in engineShowMap'
        :key="engine.name"
        :engineName="engine.name"
        :changeSearchEngine="changeSearchEngine"
      ></EngineSwitch>
      <input
        type="button"
        class="engineSettingBtn"
        value="+"
        @click="changeSettingBlockShow"
      >
    </div>

    <SettingBlock
      :changeEngineShowMap="changeEngineShowMap"
      :changeSettingBlockShow="changeSettingBlockShow"
      :engineMap="engineMap"
      v-if="isSettingBlockShow"
    ></SettingBlock>
  </div>
</template>

<script>
//搜索引擎设置框组件
import SettingBlock from '@/components/SearchBlock/SettingBlock.vue'
import EngineSwitch from '@/components/SearchBlock/EngineSwitch.vue'

export default {
  name: "SearchBlock",
  components: {
    SettingBlock,
    EngineSwitch
  },
  data() {
    return {
      //搜索内容 默认为空
      wd: "",
      //是否显示搜索引擎设置栏 默认不显示
      isSettingBlockShow: false,
      //搜索引擎的搜索api 默认百度
      searchEngineURL: "https://www.baidu.com/s?wd=",
      //可供选择的搜索引擎 name:搜索引擎名 URL:搜索引擎api
      searchEngineURLMap: [
        { name: 'Bing', URL: 'https://cn.bing.com/search?q=' },
        { name: 'Baidu', URL: 'https://www.baidu.com/s?wd=' },
        { name: 'Google', URL: 'https://www.google.com/search?q=' },
        { name: 'Bilibili', URL: 'https://search.bilibili.com/all?keyword=' },
        { name: 'Sougou', URL: 'https://www.sogou.com/web?query=' },
        { name: '360', URL: 'https://www.so.com/s?q=' },
      ],
      //可供选择的搜索引擎
      engineMap: JSON.parse(localStorage.getItem('engineMap')) || [
        { name: "Baidu", isEngineShow: true },
        { name: "Bing", isEngineShow: true },
        { name: "Bilibili", isEngineShow: true },
        { name: "Google", isEngineShow: true },
        { name: "Sougou", isEngineShow: false },
        { name: "360", isEngineShow: false },
      ],
      //显示的搜索引擎
      engineShowMap: JSON.parse(localStorage.getItem('engineShowMap')) || [
        { name: "Baidu", isEngineShow: true },
        { name: "Bing", isEngineShow: true },
        { name: "Bilibili", isEngineShow: true },
        { name: "Google", isEngineShow: true },
      ]
    };
  },
  //组件间通信：使用全局事件总线
  mounted() {
    //String:engineName 这个搜索引擎的名字
    //from:Engines组件 作为this.changeEngineMap的参数
    this.$bus.$on('engineName', this.changeEngineMap)
  },
  methods: {
    //进行一个搜索
    search() {
      window.location.href = this.searchEngineURL + this.wd;
    },
    //更改搜索引擎
    changeSearchEngine(engineName) {
      this.searchEngineURLMap.forEach((engine) => {
        if (engine.name === engineName) {
          this.searchEngineURL = engine.URL
        }
      })
    },
    //切换可供选择的搜索引擎的被选择与不被选择
    changeEngineMap(engineName) {
      this.engineMap.forEach((engine) => {
        if (engine.name === engineName) {
          engine.isEngineShow = !engine.isEngineShow
          localStorage.setItem('engineMap', JSON.stringify(this.engineMap))
        }
      })
    },
    //刷新显示的搜索引擎 （读取选择的搜索引擎并并显示）
    changeEngineShowMap() {
      this.engineShowMap = []
      this.engineMap.forEach((engine) => {
        if (engine.isEngineShow === true) {
          this.engineShowMap.push(engine)
          localStorage.setItem('engineShowMap', JSON.stringify(this.engineShowMap))
        }
      })
    },
    //切换搜索引擎设置框的显示
    changeSettingBlockShow() {
      this.isSettingBlockShow = !this.isSettingBlockShow
    },
  },
};
</script>

<style scoped>
.searchEngineURL {
  color: #7f8c8d;
  font-size: 5px;
}
#search {
  position: absolute;
  width: 100%;
  margin: auto;
  top: 150px;
  text-align: center;
}

#form {
  margin-right: 80px;
}

.searchInput {
  all: initial;
  height: 50px;
  width: 30%;
  opacity: 0.7;
  background-color: #2f3640;
  border-style: none;
  border-radius: 150px;
  border-top-right-radius: 0px;
  border-bottom-right-radius: 0px;
  color: #f4f4f4;
  font-family: 楷体;
  font-size: large;
  text-align: center;
  transition-duration: 0.5s;
}
.searchInput:hover {
  opacity: 0.95;
  box-shadow: 0 10px 50px 0px rgba(1, 1, 1);
  width: 60%;
}
.searchInput:focus {
  opacity: 1;
  background-color: #7f8c8d;
  box-shadow: 0 10px 50px 0px rgba(1, 1, 1);
  width: 60%;
}
.searchInput:focus::placeholder {
  color: #7f8c8d;
}

.searchBtn {
  position: absolute;
  height: 50px;
  width: 70px;
  border-style: none;
  opacity: 0.7;
  border-radius: 150px;
  border-top-left-radius: 0px;
  border-bottom-left-radius: 0px;
  background-color: #2f3640;
  color: #f4f4f4;
  transition-duration: 0.5s;
}
.searchBtn:hover {
  box-shadow: 0 10px 50px 0px rgba(1, 1, 1);
  opacity: 0.95;
}

.icon {
  margin-top: 12px;
  margin-left: 3px;
}
.engineSettingBtn {
  height: 30px;
  width: 70px;
  border-style: none;
  margin-top: 5px;
  margin-right: 5px;
  opacity: 0.7;
  border-radius: 150px;
  background-color: #2f3640;
  color: #f4f4f4;
  font-size: 20px;
  transition-duration: 0.5s;
  animation: slide-in-blurred-top 0.6s cubic-bezier(0.23, 1, 0.32, 1) both;
}
.engineSettingBtn:hover {
  box-shadow: 0 10px 20px 0px rgba(1, 1, 1);
  opacity: 0.95;
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
</style>
