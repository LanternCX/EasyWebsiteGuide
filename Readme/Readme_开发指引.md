# 开发指引

## 前序准备

你需要在本地安装 [node](http://nodejs.org/) 和 [git](https://git-scm.com/)。本项目技术栈基于 [ES2015+](http://es6.ruanyifeng.com/)、[vue](https://cn.vuejs.org/index.html)、[vuex](https://vuex.vuejs.org/zh-cn/)、[vue-cli](https://github.com/vuejs/vue-cli) ，提前了解这些知识会对了解本项目有很大帮助。

建议使用[vscode](https://code.visualstudio.com/)并在插件商店搜索并安装Vetur插件以打开和构建此项目,

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

