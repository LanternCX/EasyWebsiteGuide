//书签栏
<template>
  <div id='block-main'>
    <div>
      <div
        v-if="isURLInputShow"
        @mouseleave="changeInputShow()"
      >
        <input
          id="urlInput"
          type="text"
          v-model="url"
          placeholder="在此添加一个网址..."
          @keyup.enter="add()"
          autocomplete="off"
        />
        <input
          id="nameInput"
          type="text"
          v-model="name"
          placeholder="在此设置书签名称..."
          @keyup.enter="add()"
          autocomplete="off"
        />
      </div>
      <img
        id="icon_add"
        v-if="!isURLInputShow&&isGuideBlockShow"
        src="../assets/add.svg"
        width="26px"
        height="26px"
        @click="changeInputShow()"
      >
      <img
        id="icon_close"
        src="@/assets/close.svg"
        width="26px"
        height="26px"
        v-if="!isURLInputShow&&isGuideBlockShow"
        @click="changeGuideBlockShow()"
      >
      <img
        id="icon_Open"
        src="@/assets/open.svg"
        width="26px"
        height="26px"
        v-if="!isURLInputShow&&!isGuideBlockShow"
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
      >
      </GuideBox>
    </div>

  </div>
</template>

<script>
import GuideBox from './GuideBox.vue';
import { nanoid } from 'nanoid'

export default {
  name: 'GuideBlock',
  components: { GuideBox },
  data() {
    return {
      //读取书签列表&初始化书签列表（默认五个网站）
      sites: JSON.parse(localStorage.getItem('siteMap')) || [
        { id: "jsb", name: '厦一海沧团学技术', url: 'https://www.xysu.tech/' },
        { id: "xbx", name: '学不习', url: 'https://xuebuxi.cn/' },
        { id: "aio", name: '学源', url: 'https://xy.xysu.tech/' },
        { id: "xmyz", name: '厦门一中校园网', url: 'https://xmyz.xmedu.cn' },
        { id: "baidu", name: "百度", url: 'https://www.baidu.com/' }
      ],
      //初始化网页名称默认为空
      name: '',
      //初始化网页url默认为空
      url: '',
      //是否显示url输入框默认为false
      isURLInputShow: false,
      //是否显示书签栏默认为false
      isGuideBlockShow: false
    }
  },
  methods: {
    //添加书签
    add() {
      if (this.url.trim() && this.name.trim()) {
        const site = { id: nanoid(), name: this.name, url: this.url }
        this.sites.push(site);
        this.name = '';
        this.url = '';
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
    //更改url输入框的显示
    changeInputShow() {
      switch (this.isURLInputShow) {
        case (true):
          setTimeout(() => {
            this.isURLInputShow = !this.isURLInputShow;
          }, 550);
          break;
        case (false):
          this.isURLInputShow = !this.isURLInputShow;
          break;
      }
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
  height: 200px;
  top: 250px;
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

#urlInput {
  all: initial;
  height: 40px;
  width: 50px;
  opacity: 0.7;
  background-color: #2f3640;
  border-style: none;
  border-radius: 150px;
  color: #f4f4f4;
  font-family: 楷体;
  font-size: smaller;
  text-align: center;
  transition-duration: 0.5s;
  transition-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
}
#urlInput::placeholder {
  color: #2f3640;
}
#urlInput:hover::placeholder {
  color: #555;
}
#urlInput:hover {
  width: 30%;
}
#urlInput:focus {
  background-color: #7f8c8d;
}
#urlInput:focus::placeholder {
  color: #7f8c8d;
}

#nameInput {
  all: initial;
  height: 40px;
  width: 50px;
  opacity: 0.7;
  background-color: #2f3640;
  border-style: none;
  border-radius: 150px;
  color: #f4f4f4;
  font-family: 楷体;
  font-size: smaller;
  text-align: center;
  transition-duration: 0.5s;
  transition-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
}
#nameInput::placeholder {
  color: #2f3640;
}
#nameInput:hover::placeholder {
  color: #555;
}
#nameInput:hover {
  width: 30%;
}
#nameInput:focus {
  background-color: #7f8c8d;
}
#nameInput:focus::placeholder {
  color: #7f8c8d;
}
</style>