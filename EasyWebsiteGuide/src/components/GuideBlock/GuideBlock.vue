//书签栏
<template>
  <div id='block-main'>
    <div>
      <img
        id="icon_close"
        src="@/assets/close.svg"
        width="26px"
        height="26px"
        v-if="!isnameAndURLInputShow&&isGuideBlockShow"
        @click="changeGuideBlockShow()"
      >
      <img
        id="icon_Open"
        src="@/assets/open.svg"
        width="26px"
        height="26px"
        v-if="!isnameAndURLInputShow&&!isGuideBlockShow"
        @click="changeGuideBlockShow()"
      >
    </div>
    <div
      id="block-1"
      v-if="isGuideBlockShow"
    >
      <GuideBox
        v-for="site in sites"
        :key="site.id"
        :nanoid="site.id"
        :siteName="site.name"
        :url="site.url"
        :deleteSite="deleteSite"
        :isGuideBoxShow="isGuideBoxShow"
      >
      </GuideBox>
      <div
        class="addNewTag"
        @click="changeModel()"
        v-if="isGuideBoxShow"
      > <img
          src="@/assets/add.svg"
          class="icon_add"
          height="50px"
          width="50px"
        > </div>
      <div v-if="!isGuideBoxShow">
        <img
          src="@/assets/X.svg"
          class="icon_X"
          width="20px"
          height="20px"
          @click="changeModel()"
        >
        <input
          id="nameAndURLInput"
          type="text"
          v-model="url"
          placeholder="在此添加一个网址..."
          @keyup.enter="addSite()"
          autocomplete="off"
        />
        <br />
        <input
          id="nameAndURLInput"
          type="text"
          v-model="name"
          placeholder="在此设置书签名称..."
          @keyup.enter="addSite()"
          autocomplete="off"
        />
      </div>
    </div>

  </div>
</template>

<script>
import GuideBox from '@/components/GuideBlock/GuideBox.vue';
import { nanoid } from 'nanoid'

export default {
  name: 'GuideBlock',
  components: { GuideBox },
  data() {
    return {
      //读取书签列表&初始化书签列表 默认五个网站
      sites: JSON.parse(localStorage.getItem('siteMap')) || [
        { id: "jsb", name: '厦一海沧团学技术', url: 'https://www.xysu.tech/' },
        { id: "xbx", name: '学不习', url: 'https://xuebuxi.cn/' },
        { id: "aio", name: '学源', url: 'https://xy.xysu.tech/' },
        { id: "xmyz", name: '厦门一中校园网', url: 'https://xmyz.xmedu.cn' },
      ],
      //初始化网页名称 默认为空
      name: '',
      //初始化网页url 默认为空
      url: '',
      //是否显示url输入框 默认为false
      isnameAndURLInputShow: false,
      //是否显示书签栏 默认为false
      isGuideBlockShow: false,
      //是否为书签模式 默认为true
      isGuideBoxShow: true
    }
  },
  methods: {
    //添加书签
    addSite() {
      if (this.url.trim() && this.name.trim()) {
        const site = { id: nanoid(), name: this.name, url: this.url }
        this.sites.push(site);
        this.name = '';
        this.url = '';
        this.changeModel();
      } else {
        return alert('输入不能为空');
      }
    },
    //删除书签
    deleteSite(nanoid) {
      if (confirm("删除这个书签?")) {
        this.sites = this.sites.filter((site) => {
          return site.id !== nanoid;
        })
      }
    },
    //在添加书签和显示书签之间切换
    changeModel() {
      console.log(1);
      this.isGuideBoxShow = !this.isGuideBoxShow
    },
    //更改整个书签框的显示
    changeGuideBlockShow() {
      this.isGuideBlockShow = !this.isGuideBlockShow;
    }
  },
  watch: {
    //更新书签表
    sites() {
      localStorage.setItem('siteMap', JSON.stringify(this.sites))
    }
  },
}
</script>

<style>
#block-main {
  position: absolute;
  height: 0px;
  top: 260px;
  width: 100%;
  text-align: center;
  transition: 0.5s;
  transition-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
}

#block-1 {
  width: 550px;
  height: 350px;
  border-radius: 30px;
  text-align: center;
  display: inline-block;
  overflow: auto;
  background-color: rgba(244, 244, 244, 0.1);
  backdrop-filter: blur(5px);
  box-shadow: 0 10px 10px 5px rgba(1, 1, 1, 0.4);
  animation: scale-in-top 0.15s cubic-bezier(0.25, 0.46, 0.45, 0.94) both;
}
/* 隐藏了滚动条 */
::-webkit-scrollbar {
  width: 0px;
}
@keyframes scale-in-top {
  0% {
    -webkit-transform: scale(0);
    transform: scale(0);
    -webkit-transform-origin: 50% 0%;
    transform-origin: 50% 0%;
    opacity: 1;
  }
  100% {
    -webkit-transform: scale(1);
    transform: scale(1);
    -webkit-transform-origin: 50% 0%;
    transform-origin: 50% 0%;
    opacity: 1;
  }
}

#nameAndURLInput {
  all: initial;
  height: 40px;
  width: 30%;
  opacity: 0.7;
  margin-top: 5px;
  background-color: #2f3640;
  border-style: none;
  border-radius: 150px;
  color: #f4f4f4;
  font-family: 楷体;
  font-size: smaller;
  text-align: center;
  transition-duration: 0.5s;
  transition-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
  animation: slide-in-blurred-top 0.3s cubic-bezier(0.23, 1, 0.32, 1) both;
}
#nameAndURLInput::placeholder {
  color: #555;
}
#nameAndURLInput:hover {
  box-shadow: 0 5px 10px 0px rgba(1, 1, 1, 0.4);
}
#nameAndURLInput:focus {
  background-color: #7f8c8d;
}
#nameAndURLInput:focus::placeholder {
  color: #7f8c8d;
}

.addNewTag {
  height: 100px;
  width: 100px;
  float: left;
  margin: 10px 5px 0 5px;
  background-color: rgba(47, 54, 64, 0.4);
  border-radius: 15px;
  transition: 0.5s;
  box-shadow: 0 5px 10px 0px rgba(1, 1, 1, 0.4);
  animation: slide-in-blurred-top 0.3s cubic-bezier(0.23, 1, 0.32, 1) both;
}
.addNewTag:hover {
  background-color: #7f8c8d;
  opacity: 0.9;
}

.icon_add {
  height: 40px;
  width: 40px;
  margin-top: 30px;
  transition: 0.5s;
  transition-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
}
.icon_add:hover {
  height: 60px;
  width: 60px;
  margin-top: 20px;
}
@keyframes slide-in-blurred-right {
  0% {
    width: 100px;
    height: 0;
    right: 0;
    filter: blur(40px);
    opacity: 0;
  }
  100% {
    width: 200px;
    height: 100%;
    filter: blur(0);
    opacity: 1;
  }
}
</style>