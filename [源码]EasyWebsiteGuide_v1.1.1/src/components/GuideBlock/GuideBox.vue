//单个网址书签组件
<template>
  <div
    id='guide'
    v-if="isGuideBoxShow"
  >
    <div>
      <img
        id="delete"
        src="@/assets/trash.svg"
        width="30px"
        height="30px"
        v-if="isDeleteBtnShow"
        @click="removeSite()"
        @mouseleave="changeDeleteBtnShow()"
      >
      <a :href="url">
        <img
          id="icon"
          v-if="!isDeleteBtnShow"
          :src="iconURL"
          @click.right="changeDeleteBtnShow()"
          @error="defaultImgs()"
        >
      </a>
      <h6 v-if="!isDeleteBtnShow"> {{siteName}} </h6>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GuideBox',
  //String:站点名，methods:删除该标签,String:标签nanoid，Stiring:标签指向的URL
  props: ['siteName', 'deleteSite', 'nanoid', 'url', 'isGuideBoxShow'],
  data() {
    return {
      //网站icon的url
      iconURL: this.url + '/favicon.ico',
      //是否显示删除按钮
      isDeleteBtnShow: false
    }
  },
  methods: {
    //删除书签
    removeSite() {
      this.deleteSite(this.nanoid);
    },
    //图标获取失败切换默认图标，给xuebuxi.cn写了特判
    defaultImgs() {
      this.iconURL = require("@/assets/tag.svg" || "@/assets/tag.png" || "@/assets/tag.jpg");
      if (this.url == "https://xuebuxi.cn/") {
        this.iconURL = require("@/assets/xuebuxi.png");
      }
    },
    //切换书签icon和垃圾桶icon(同时切换功能)
    changeDeleteBtnShow() {
      document.oncontextmenu = function () {
        return false;
      }
      this.isDeleteBtnShow = !this.isDeleteBtnShow;
    }
  }
}
</script>
 
<style>
#guide {
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
#guide:hover {
  background-color: #7f8c8d;
  opacity: 0.9;
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
    opacity: 1;
  }
}
#icon {
  height: 40px;
  width: 40px;
  margin-top: 30px;
  transition: 0.5s;
  transition-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
}
#icon:hover {
  height: 60px;
  width: 60px;
  margin-top: 20px;
}

#delete {
  height: 30px;
  width: 30px;
  margin-top: 35px;
  transition: 0.5s;
  transition-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1);
}
#delete:hover {
  height: 60px;
  width: 60px;
  margin-top: 20px;
}
h6 {
  margin: 0 auto;
  color: #f4f4f4;
}
</style>