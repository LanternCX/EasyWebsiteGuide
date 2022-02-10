## 简介

[EasyWebsiteGuide](https://github.com/CDBxinhe/EasyWebsiteGuide)是一个简单易上手的用于网址导航的网页，它基于开源框架[vue.js](https://github.com/vuejs)实现，基于`vue-cli`工具进行构建，是一个纯前端项目。它支持添加URL书签以进行快捷的网址导航，在搜索框内进行默认的百度搜索。相信这个项目可以方便你访问、收藏、管理网址。

- [开源地址](https://github.com/CDBxinhe/EasyWebsiteGuide)
- [视频介绍](https://www.bilibili.com/video/BV1Fr4y1a7DH)

## 前序准备

你需要在本地安装 [node](http://nodejs.org/) 和 [git](https://git-scm.com/)。本项目技术栈基于 [ES2015+](http://es6.ruanyifeng.com/)、[vue](https://cn.vuejs.org/index.html)、[vuex](https://vuex.vuejs.org/zh-cn/)、[vue-cli](https://github.com/vuejs/vue-cli) ，提前了解这些知识会对了解本项目有很大帮助。

## 功能

```
- 在搜索框进行搜索

- 下拉式的隐藏书签栏
 - 添加网页URL和设置网页书签名称以添加一个书签
 - 右键删除以该书签

```

## 开发

```bash
# 克隆项目
git clone https://github.com/CDBxinhe/EasyWebsiteGuide.git

# 进入项目文档
cd EasyWebsiteGuide/EasyWebsiteGuide

# 安装依赖
npm install

# 建议不要直接使用 cnpm 安装依赖，会有各种诡异的 bug。可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npm.taobao.org

# 启动服务
npm run serve

```

浏览器访问 http://localhost:8080

## 发布

```bash
# 打包项目
npm run build
```

## 其他

```bash
# 代码格式检查
npm run lint
```

