---
title: 使用 VAQ 开发移动端应用
date: 2020-05-17 12:54:15
categories: 知识分享 | 视频类
tags: [KnowledgeSharing, Vue, APICloud]
---

使用 Hybrid 开发移动端应用，现在有例如 `Ionic`，`uni-app`，`APICloud` 等众多解决方案。其中 `Ionic` 最开始以 `Angular` 为开发框架，后来也实现了 `React` 和 `Vue` 的版本；`uni-app` 隶属于 `DCloud`，涉及 PC Web 端，各大小程序，移动端 APP 等，几乎包揽了整个大前端， 其生态发展也在日益扩大; `APICloud` 专注于`融合`, 将原生模块的功能以 `API` 的形式融合到前端开发中，提供了开发者无限扩展的空间。今天就主要以 `APICloud` 为例，介绍如何使用 VAQ （Vue-APICloud-Quickstart）开发移动端应用。

阅读下文，需要如下前备知识：
- 基础的前端开发知识
- 使用 APICloud 开发 APP 的基础知识
- Vue.js 框架的基本使用
- 知道 Typescript

首先我们需要在 APICloud 平台控制台创建应用，配置好 “端设置” 和 “证书”, 在 “模块” 中选择自己要用到模块后，在 “自定义 loader” 中编译自定义 loader 并下载安装。

然后我们在本地 使用 vue cli 创建一个新的 vue 项目，姑且命名为 vaq-project。
如果我们习惯于 ts 开发，则在创建项目的时候可以选择 `Typescript`。

```bash
vue create vaq-project
```

然后我们切入到项目下安装 VAQ 框架，

```bash
cd vaq-project
vue add @w-xuefeng/apicloud
```

将会自动识别是否使用 `Typescript`，并生成对应的开发模版目录

接着会提示我们输入一些信息，我们按照提示输入即可

```bash
? 请输入项目 ID (Please enter the app id of your project) A6000000000001
? 请输入项目名称 (Please enter the app name of your project) vue-apicloud-template
? 请输入项目描述 (Please enter the description of your project) A Vue.js APP with APICloud
? 请输入项目作者 (Please enter the author of your project) @w-xuefeng/vue-cli-plugin-apicloud
? 请输入运行项目的端口号，默认 8080 (Please enter the port number of the running project, the default is 8080) 8080
```

值得注意的是，APICloud 项目 ID 与 自定义 loader 的项目 ID 是一致的，否则无法进行 WiFi 调试。若 8080 端口已经被其他程序占用，我们应该输入一个新的未被占用的端口号。 安装完成后，如果要修改端口号，我们不仅要修改 package.json 中

```json
"serve": "vue-cli-service serve --port 8080"
```

的端口号，还要修改 index.html 中 

```js
url: 'http://192.168.XX.XX:8080/indexindex.html'
```

中的端口号，然后重启项目并执行一次 WiFi 同步。同样的，在 WiFi 调试的时候，如果我们的本地 IP 发生了变化的话，需要修改 index.html 中 

```js
url: 'http://192.168.XX.XX:8080/indexindex.html'
```

中的 IP 地址，然后执行一次 WiFi 同步。

安装完 VAQ 之后，项目的目录结构会发生变化，如下

```
.
├── public                   # 静态资源
│   ├── index.html           # 页面模板
│   └── res                  # 静态资源
├── src
│   ├── pages                # 页面入口
│   └── config               # 配置入口
|       └── pages.json       # 页面配置
├── index.html               # APP入口
├── config.xml               # APICloud 项目配置文件
├── .syncignore              # APICloud wifi 同步忽略文件
├── ...
└── package.json

```

我们想要在 src/pages 目录下新建页面时，必须要在 src/config/pages.json 中配置相关参数才能生效。
查看默认的 `src/config/pages.json`, 会发现项目里有四个示例页面：

```json
[
  {
    "title": "开屏广告页",
    "name": "index",
    "path": "index/index"
  },
  {
    "title": "登录页",
    "name": "login",
    "path": "login/index"
  },
  {
    "title": "应用首页",
    "name": "home",
    "path": "home/index"
  },
  {
    "title": "web页面",
    "name": "web",
    "path": "home/web"
  }
]
```

其中 `title` 是页面 HTML 文件的标题， `name` 是页面 `window` 或 `Frame` 的 `name`，`path` 是页面文件相对于 `src/pages` 目录的路径。我们可以修改或者删除默认页面的配置及对应文件夹下的页面文件，然后添加我们自己的页面。

接下来我们启动项目, 看看示例页面。不过，在启动项目之前，值得我们注意的是，在 main.js 或 main.ts (如果创建项目的时候使用了 Typescript)中，有如下配置

```js
Vue.use(VAQ,
  {
    pages,
    debugOnPC: process.env.NODE_ENV !== 'production '
  }
).init({ el: '#app', render: h => h(App) })
```
其中 `pages` 便是上面的 `src/config/pages.json`, `debugOnPC` 则为是否在 PC端 调试的开关。众所周知，在 loader 和正式应用中, APICloud 会融合原生模块的功能到 `window.api` 中，而在 PC 端是没有 `api` 能力的。 所以当我们将 `debugOnPC` 设置为 `true` 时，我们仅仅只能在 PC 浏览器端调试样式和界面结构。如果我们不设置 `debugOnPC` 或者设置为`false` 时，PC 端将无法查看页面，这是因为 `new Vue()` 的操作被放到了 `apiready` 的回调中了，PC 端默认是没有 `apiready` 这个事件的。

我们将 `debugOnPC` 设置为 `process.env.NODE_ENV !== 'production '`，然后执行以下命令启动项目

```bash
npm run serve
```
我们首先在 PC 浏览器端查看示例界面，打开默认的地址`http://localhost:8080`，是页面导航页，如下图所示：

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/vaq/1.png" width="100%">

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/vaq/2.png" width="100%">

该页面显示了我们项目中所有的页面配置，点击对应的页面则会跳转（若页面之间有参数传递，则通过页面导航打开将不会传递任何参数）。导航页面仅做为页面结构和样式调试时快速打开对应页面使用，自定义 Loader 中将不会展示本页面。

- 默认的`开屏广告页`
- `path` 为 `index/index`
- 对应编译后的地址为`indexindex.html`
- 如下图所示

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/vaq/3.png" width="100%">

- 点击屏幕中的按钮，将跳转到默认的`登录页`
- `path` 为 `login/index`，
- 对应编译后的地址为`loginindex.html`
- 如下图所示

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/vaq/4.png" width="100%">

- 根据提示输入用户名和密码，点击登录，将跳转到默认`应用首页`
- `path` 为 `home/index`，
- 对应编译后的地址为`homeindex.html`
- 登录后退出应用再次打开，默认保留登录状态，将直接回到本页面
- 如下图所示

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/vaq/5.png" width="100%">

- 点击任意链接，在自定义 Loader 中将在新窗口打开而PC 浏览器将会直接跳转到默认的`web页面`，并载入网页链接内容
- `path` 为 `home/web`，
- 对应编译后的地址为`homeweb.html`
- 如下图所示

<img src="https://pub.wangxuefeng.com.cn/asset/blogthumbnail/vaq/6.png" width="100%">

以上便是所有默认示例页面的展示。示例页面仅仅是向开发者举例页面的开发方式，并不能用在正式项目中，所以开发者应将示例页面删除并新建自己项目的页面，或者直接修改为自己项目的页面。

在 PC 端调试时，我们可以在浏览器中输入 `/webpack-dev-server` 查看编译后的文件目录结构, 默认如下所示

```
.
├── js
│   ├── chunk-vendors.js
│   ├── indexindex.js
│   ├── loginindex.js
│   ├── homeindex.js
│   └── homeweb.js
├── index.html
├── indexindex.html
├── loginindex.html
├── homeindex.html
├── homeweb.html
├── favicon.ico
├── res
│    └── img
│         └── logo.png

```

其中 index.html 为导航页面，仅用于 PC 浏览器端调试页面，Loader 调式和生成 Widget 时将会忽略该页面。


关于具体开发问题，详见[VAQ文档](https://vaq.wangxuefeng.com.cn)。