## 1. vite

![搭建vite项目](vue3搭建.assets/搭建vite项目.png)

## 2. prettier

### 2.1 安装

```bash
npm install --save-dev prettier
```

### 2.2 配置

新建`.prettierrc.cjs`

```js
module.exports = {
    // 使用单引号而不是双引号。
    singleQuote: true,
    // 打印宽度设置为 100，这意味着当代码行长度超过 100 个字符时，
    // Prettier 会自动换行。
    printWidth: 100,
    // 使用 2 个空格作为缩进单位。
    tabWidth: 2,
    // 不使用制表符进行缩进。
    useTabs: false,
    //句末使用分号
    semi: true,
    // 会移除多行对象或数组的尾随逗号
    trailingComma: 'none',
    // 根据运行环境自动选择最合适的换行符
    endOfLine: 'auto'
}
```

### 2.3 配置script

```json
"scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "format": "prettier --write ."
},
```

## 3. eslint

### 3.1 安装

```bash
npm install --save-dev eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-vue
```

### 3.2 配置

新建`.eslintrc.cjs`

```js
module.exports = {
  // 指定此配置文件为根配置文件，ESLint 将停止在父目录中查找配置。
  root: true,
  // 指定环境，这里设置为 Node.js 环境
  env: {
    node: true
  },
  // 指定解析器，这里使用 vue-eslint-parser 解析 Vue 文件
  parser: 'vue-eslint-parser',
  parserOptions: {
    ecmaVersion: 2018, // 指定要使用的 ECMAScript 版本
    sourceType: 'module', // 设置为 "module" 表示 ECMAScript 模块
    jsxPragma: 'React', // 指定在 JSX 文件中使用的 pragma，默认为 "React"
    ecmaFeatures: {
      jsx: true // 启用 JSX 支持
    }
  },
  // 扩展规则，这里使用了一些推荐的规则集和插件
  extends: [
    'plugin:vue/vue3-recommended', // Vue.js 推荐规则
    'plugin:prettier/recommended', // Prettier 推荐规则
    'eslint-config-prettier' // 禁用与 Prettier 冲突的 ESLint 规则
  ],
  // 自定义规则
  rules: {
    // 在这里添加或修改规则
    'space-before-function-paren': 'off', // 关闭函数参数前的空格规则
    'no-use-before-define': 'off', // 禁止定义之前使用变量
    'no-unused-vars': [
      // 禁止未使用的变量
      'error',
      {
        argsIgnorePattern: '^_', // 忽略以下划线开头的参数
        varsIgnorePattern: '^_' // 忽略以下划线开头的变量
      }
    ],
    'vue/comment-directive': 'off', // 关闭注释指令
    'vue/script-setup-uses-vars': 'error', // Vue3 `<script setup>` 必须使用的变量
    'vue/multi-word-component-names': 'off', // 关闭多个单词组件名
    'vue/custom-event-name-casing': 'off', // 关闭自定义事件名称大小写
    'vue/attributes-order': 'off', // 关闭属性排序
    'vue/one-component-per-file': 'off', // 关闭每个文件只有一个组件
    'vue/html-closing-bracket-newline': 'off', // 关闭 HTML 标签闭合括号的换行
    'vue/max-attributes-per-line': 'off', // 关闭每行最大属性数
    'vue/multiline-html-element-content-newline': 'off', // 关闭多行 HTML 元素内容的换行
    'vue/singleline-html-element-content-newline': 'off', // 关闭单行 HTML 元素内容的换行
    'vue/attribute-hyphenation': 'off', // 关闭属性连字符命名
    'vue/require-default-prop': 'off', // 关闭要求默认的属性
    'vue/html-self-closing': [
      // 要求或禁止自我关闭的标签
      'error',
      {
        html: {
          void: 'always', // 要求对 HTML 中的空元素进行自我关闭
          normal: 'never', // 不要求对普通元素进行自我关闭
          component: 'always' // 要求对组件进行自我关闭
        },
        svg: 'always', // 要求对 SVG 元素进行自我关闭
        math: 'always' // 要求对 MathML 元素进行自我关闭
      }
    ]
  }
};
```

### 3.3 配置script

```json
"scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "format": "prettier --write .",
    "lint": "eslint src --fix"
},
```

## 4. 安装Element Plus

官网`https://element-plus.gitee.io/zh-CN/guide/installation.html`

```bash
npm install element-plus --save

npm install @element-plus/icons-vue // 看需求
```

### 4.1 按需导入

首先你需要安装`unplugin-vue-components` 和 `unplugin-auto-import`这两款插件

```bash
npm install -D unplugin-vue-components unplugin-auto-import
```

然后把下列代码插入到你的 `Vite` 或 `Webpack` 的配置文件中

```ts
// vite.config.ts
import { defineConfig } from 'vite'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  // ...
  plugins: [
    // ...
    AutoImport({
      resolvers: [ElementPlusResolver()],
    }),
    Components({
      resolvers: [ElementPlusResolver()],
    }),
  ],
})
```

### 4.2 安装SCSS

官网`https://sass-lang.com`

```bash
npm install sass -D
```

不需要安装`sass-loader`和`node-sass`

## 5. 安装tailwind css

官网`https://www.tailwindcss.cn`

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

`tailwind.config.js`

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx,vue}", // 这里记得加上vue，官网直接拷贝过来是没有的
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}

// 配置px和font-size https://blog.csdn.net/m0_37890289/article/details/134875605
// 或者写mr-[16px] => margin-right: 16px
```

PostCSS 是一个工具，用于转换 CSS 代码。它可以帮助你在编写 CSS 时使用未来的 CSS 语法，并将其转换为当前所有浏览器都支持的语法。同时，它还支持许多插件，可以用来执行各种任务，例如添加浏览器前缀、压缩代码、处理嵌套样式等。

**Tailwind CSS**：是一个实用的 CSS 框架，它提供了一组可复用的样式工具类，帮助你更快地构建界面。

**Autoprefixer**：是一个 PostCSS 插件，用于自动添加浏览器前缀。它可以根据 Can I Use 网站上的数据，自动为你的 CSS 添加适当的前缀，以确保你的样式在不同浏览器中都能正常工作。

接着，你需要在你的项目中创建一个 PostCSS 配置文件（如果你还没有创建的话）。可以创建一个名为 `postcss.config.js` 的文件，并在其中配置 PostCSS 插件，例如：

## 6. 重置样式文件

### 6.1 安装normalize.css

```bash
npm install normalize.css
```

### 6.2 创建styles文件夹

**index.scss**

```scss
// 组织统一导出 
@use 'normalize.css';
@use './transition.scss';
@use './nprogress.scss';
@use "./variable.scss";

@tailwind base;
@tailwind components;
@tailwind utilities;
```

**variable.scss**

```scss
// 项目提供scss全局变量

/** 滚动条相关变量-开始 [滚动条在@/assets/index.scss]） */
// 横部滚动条宽，纵向滚动条高
$webkit-scrollbar-width: 6px;
$webkit-scrollbar-height: 6px;

// 滚动条圆角
$webkit-scrollbar-border-radius: 10px;

// 滚动条颜色(已使用)
$webkit-scrollbar-color: var(--el-color-primary-light-3); // (已使用)
$webkit-scrollbar-hover-color: var(--el-color-primary); // (已使用)

/** 滚动条相关变量-结束 */

/** Aside左侧布局相关变量-开始 */
// 左侧布局层级
$layout-aside-z-index: 10;

// Logo和标题高度
$aside-header-height: 56px;

// 左侧菜单高度
$aside-menu-height: 40px; // (已使用)[页面：@/layouts/components/Menu/SubMenu.vue]
// 左侧菜单字体 AND 图标左侧偏移
$aside-menu-font-icon-translate: -8px; // (已使用)[页面：@/layouts/components/Menu/SubMenu.vue]
// 左侧菜单菜单字体加粗
$aside-menu-font-weight: 500;

// 左侧菜单间隔
$aside-menu-margin-bottom: 3px;

// 左侧菜单边框圆角配置
$aside-menu-border-left: 6px;

// 左侧菜单左内边框宽度
$aside-menu-padding-left: 2px;

// 左侧菜单右内边框宽度
$aside-menu-padding-right: 2px;

// 左侧菜单右阴影
$aside-menu-box-shadow: 2px 0 12px #1d23290d;

/** Aside左侧布局相关变量-结束 */

/** Column双栏布局相关变量-开始 */
// 左侧菜单左内边框宽度[双栏布局]
$column-menu-padding-left: 4px;

// 左侧菜单右内边框宽度[双栏布局]
$column-menu-padding-right: 4px;

// 双栏布局最左侧第一个右阴影
$column-menu-box-shadow: 2px 0 12px #1d23290d inset;

/** Column双栏布局相关变量-结束 */
```

**transition.scss**

```scss
/* 默认 */
.fade-default-enter-active,
.fade-default-leave-active {
  transition: opacity 0.2s ease-in-out;
}
.fade-default-enter-from,
.fade-default-leave-to {
  opacity: 0;
}

/* fade */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease-in-out;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* fade-slide */
.fade-slide-leave-active,
.fade-slide-enter-active {
  transition: all 0.3s;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* fade-bottom */
.fade-bottom-enter-active,
.fade-bottom-leave-active {
  transition:
    opacity 0.25s,
    transform 0.3s;
}
.fade-bottom-enter-from {
  opacity: 0;
  transform: translateY(-10%);
}
.fade-bottom-leave-to {
  opacity: 0;
  transform: translateY(10%);
}

/* fade-scale */
.fade-scale-leave-active,
.fade-scale-enter-active {
  transition: all 0.28s;
}
.fade-scale-enter-from {
  opacity: 0;
  transform: scale(1.2);
}
.fade-scale-leave-to {
  opacity: 0;
  transform: scale(0.8);
}

/* zoom-fade */
.zoom-fade-enter-active,
.zoom-fade-leave-active {
  transition:
    transform 0.2s,
    opacity 0.3s ease-out;
}
.zoom-fade-enter-from {
  opacity: 0;
  transform: scale(0.92);
}
.zoom-fade-leave-to {
  opacity: 0;
  transform: scale(1.06);
}
```

**nprogress.scss**

```scss
/* nprogress进度条颜色配置 */
#nprogress .bar {
  background: var(--el-color-primary) !important;
}

#nprogress .spinner-icon {
  border-top-color: var(--el-color-primary) !important;
  border-left-color: var(--el-color-primary) !important;
}
#nprogress .peg {
  box-shadow:
    0 0 10px var(--el-color-primary),
    0 0 5px var(--el-color-primary) !important;
}
```

### 6.3 在main.js中引入

```js
// main.js

import { createApp } from 'vue';
import './styles/index.scss';
import App from './App.vue';

createApp(App).mount('#app');
```

### 6.4 删除原始带的组件

`无示例`

### 6.5 配置vite别名和scss变量

```js
import { defineConfig } from 'vite';
import vue from '@vitejs/plugin-vue';
import AutoImport from 'unplugin-auto-import/vite';
import Components from 'unplugin-vue-components/vite';
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers';
import path from 'path';

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    AutoImport({
      resolvers: [ElementPlusResolver()]
    }),
    Components({
      resolvers: [ElementPlusResolver()]
    })
  ],
  resolve: {
    // 配置路径别名
    alias: {
      '@': path.resolve('./src'), // 相对路径别名配置，使用 @ 代替 src
      '~': path.resolve('./src')
    }
  },
  css: {
    // css全局变量使用，@/styles/variable.scss文件
    preprocessorOptions: {
      scss: {
        javascriptEnabled: true,
        additionalData: '@import "./src/styles/variable.scss";'
      }
    }
  }
});

```

### 6.6 创建config文件夹

**index.js**

```js
// 全局默认配置项
// 首页地址（默认）
export const HOME_URL: string = "/home/index";

// 登录页地址（默认）
export const LOGIN_URL: string = "/login";

// pinia仓库前缀
export const PINIA_PREFIX: string = "iqoo-";

// Svg本地图片使用 koi- 开头才会生效
export const SVG_PREFIX: string = "iqoo-";

// 默认主题颜色
export const DEFAULT_THEME: string = "#2992FF";

// 路由白名单地址（本地存在的路由 staticRouter.ts 中）
export const ROUTER_WHITE_LIST: string[] = ["/500"];
```

### 6.7 创建.env.xxx

**.env.development**

```txt 
# 变量必须以 VITE_ 为前缀才能暴露给外部读取
NODE_ENV = 'development'
VITE_WEB_TITLE = 'KOI-ADMIN'
VITE_WEB_BASE_API = '/dev-api'
# 本地Mock地址
VITE_SERVER = 'http://localhost:8088'
# 路由模式[哈希模式 AND WEB模式 [hash | history, 这两个模式是固定死的，不能乱改值]
VITE_ROUTER_MODE = history
# 是否使用全部去除console和debugger
VITE_DROP_CONSOLE = false
```

**.env.production**

```txt
# 变量必须以 VITE_ 为前缀才能暴露给外部读取
NODE_ENV = 'production'
VITE_WEB_TITLE = 'YU-ADMIN'
VITE_WEB_BASE_API = '/prod-api'
# 后端接口地址
VITE_SERVER = 'https://39.107.143.109:8088'
# 路由模式[哈希模式 AND WEB模式 [hash | history, 这两个模式是固定死的，不能乱改值]
VITE_ROUTER_MODE = history
# 是否使用全部去除console和debugger
VITE_DROP_CONSOLE = true
```



## 7. pinia

### 7.1 安装pinia和持久化插件

```bash
npm install pinia 
npm install pinia-plugin-persistedstate
```

### 7.2 创建stores文件夹

**index.js**

```js
// 创建大仓库
import { createPinia } from 'pinia';
// pinia持久化
import piniaPluginPersistedstate from 'pinia-plugin-persistedstate';
// createPinia方法可以用于创建大仓库
const pinia = createPinia();
pinia.use(piniaPluginPersistedstate);
// 对外暴露,安装仓库
export default pinia;
```

**创建stores/modules**



## 8. 路由

### 8.1 安装

```bash
npm install vue-router@4
```

### 8.2 创建utils文件夹

**安装nprogress**

```bash
npm install --save nprogres
```

**nprogress.js**

```js
import NProgress from 'nprogress';
import 'nprogress/nprogress.css';

NProgress.configure({
  easing: 'ease', // 动画方式
  speed: 500, // 递增进度条的速度
  showSpinner: true, // 是否显示加载ico
  trickleSpeed: 200, // 自动递增间隔
  minimum: 0.3 // 初始化时的最小百分比
});

export default NProgress;

```

### 8.3 创建routers文件夹

**modules/dynamicRouter.ts**

```js
// 可以先不研究用这个，先用静态路由做演示，以后再扩展

import useUserStore from "@/stores/modules/user.ts";
import useAuthStore from "@/stores/modules/auth.ts";

import { LOGIN_URL } from "@/config/index.ts";
// TS OR JS 中不能直接导入 import { useRouter } from "vue-router";
import router from "@/routers/index";

// const modules = import.meta.glob("@/views/**/*.vue");

export const initDynamicRouter = async () => {
  const userStore = useUserStore();
  const authStore = useAuthStore();

  try {
    // 1、获取菜单列表 && 按钮权限列表 && 递归菜单数据
    await authStore.listRouters();
    await authStore.getLoginUserInfo();

    // 2、判断当前用户是否拥有菜单权限
    console.log("authStore.menuList", authStore.menuList);
    // Proxy对象转换为正常的JSON数据
    // const menuRouters = JSON.parse(JSON.stringify(authStore.menuList));
    if (authStore.menuList == null || authStore.menuList.length == 0) {
      userStore.setToken("");
      router.replace(LOGIN_URL);
      return;
    }

    // 3、添加动态路由[扁平化一级路由数据]
    authStore.menuList.forEach((item: any) => {
      // if (item.component && typeof item.component == "string") {
      //   // 扁平化路由也需要构造component路由函数
      //   item.component = modules["/src/views/" + item.component + ".vue"];
      // }
      if (item.isFull == "0") {
        // 如果是全屏的话，直接为整个页面
        router.addRoute(item);
      } else {
        router.addRoute("layout", item);
      }
    });
  } catch (error) {
    console.log(error);
    // 当菜单请求出错时，重定向到登陆页
    userStore.setToken("");
    router.replace(LOGIN_URL);
    return Promise.reject(error);
  }
};
```

**modules/staticRouter.ts**

```js
```



**index.js**

```js
// 简单实现一下，用来测试

import { createRouter, createWebHashHistory, createWebHistory } from 'vue-router';
import nprogress from '@/utils/nprogress';
import { LOGIN_URL, ROUTER_WHITE_LIST } from '@/config/index.js';

// .env配置文件读取
const mode = import.meta.env.VITE_ROUTER_MODE;

// 路由访问两种模式：带#号的哈希模式，正常路径的web模式。
const routerMode = {
  hash: () => createWebHashHistory(),
  history: () => createWebHistory()
};

// 创建路由器对象
const router = createRouter({
  // 路由模式hash或者默认不带#
  history: routerMode[mode](),
  routes: [],
  strict: false,
  // 滚动行为
  // scrollBehavior 函数返回了一个对象,指定了页面在导航到新路由时应该滚动到页面的顶部 (left: 0, top: 0)
  scrollBehavior() {
    return {
      left: 0,
      top: 0
    };
  }
});

/**
 * @description 前置路由
 */
router.beforeEach(async (to, from, next) => {
  // const userStore = useUserStore();
  // const authStore = useAuthStore();

  // 1、NProgress 开始
  nprogress.start();

  // 2、标题切换，没有防止后置路由，是因为页面路径不存在，title会变成undefined
  // const title = import.meta.env.VITE_WEB_TITLE;
  // document.title = to.meta.title || title;

  // 3、判断是访问登陆页，有Token访问当前页面，token过期访问接口，axios封装则自动跳转登录页面，没有Token重置路由到登陆页。
  if (to.path.toLocaleLowerCase() === LOGIN_URL) {
    // 有Token访问当前页面
    // if (userStore.token) {
    //   return next(from.fullPath);
    // } else {
    //   koiMsgWarning('账号身份已过期，请重新登录🌻');
    // }
    // 没有Token重置路由到登陆页。
    // resetRouter();
    return next();
  }

  // 4、判断访问页面是否在路由白名单地址[静态路由]中，如果存在直接放行。
  if (ROUTER_WHITE_LIST.includes(to.path)) return next();

  // 5、判断是否有 Token，没有重定向到 login 页面。
  // if (!userStore.token) return next({ path: LOGIN_URL, replace: true });

  // 6、如果没有菜单列表[一级扁平化路由 OR 递归菜单路由数据判断是否存在都阔以]，就重新请求菜单列表并添加动态路由。
  // if (!authStore.getMenuList.length) {
  // 注意：authStore.getMenuList，不能持久化菜单数据，否则这里一直有值，就不会走这里，而且持久化之后还会被篡改数据。
  // 获取相关菜单数据 && 按钮数据 && 角色数据 && 用户信息。
  // console.log("刷新页面");
  // await initDynamicRouter();
  // return next({ ...to, replace: true }); // ...to 保证路由添加完了再进入页面 (可以理解为重进一次) replace: true 重进一次, 不保留重复历史
  // }
  // 7、正常访问页面。
  next();
});

/**
 * @description 重置路由
 */
// export const resetRouter = () => {
//   const authStore = useAuthStore();
//   authStore.getMenuList.forEach((route) => {
//     const { name } = route;
//     if (name && router.hasRoute(name)) {
//       router.removeRoute(name);
//     }
//   });
// };

/**
 * @description 路由跳转错误
 */

router.onError((error) => {
  // 结束全屏动画
  nprogress.done();
  console.warn('路由错误', error.message);
});

/**
 * @description 后置路由
 */
router.afterEach(() => {
  // console.log("后置守卫", to, from);
  // 结束全屏动画
  nprogress.done();
});

export default router;
```

### 8.4 引入main.js

```js
// 引入路由
import router from "./routers";

// 引入仓库pinia
import pinia from "./stores/index.ts";

// 创建app
const app = createApp(App);

// 注册路由
app.use(router);

// 注册pinia
app.use(pinia);

// 挂载
app.mount("#app");
```

## 9. utils

### 9.1 tool

**utils/tool.js**

```js
import { ElMessage, MessageHandler } from 'element-plus'

/**
 * @description 文档注册enter事件
 * @param {Function} cb
 * @return {void}
 */
export function handleEnter(cb: Function): void {
  if (typeof cb !== 'function')
    return

  document.onkeydown = (e) => {
    const ev: KeyboardEventInit = e || window.event
    const keyCode = ev.code || ev.keyCode
    if (keyCode === 'Enter' || keyCode === 13)
      cb()
  }
}

/**
 * @description 日期格式化
 * @param {string | number} time {string like：{y}-{m}-{d} {h}:{i}:{s} } pattern
 * @return {string}
 */
export function parseTime(time: string | number, pattern: string) {
  if (arguments.length === 0 || !time)
    return null

  const format = pattern || '{y}-{m}-{d}'
  let date
  if (typeof time === 'object') {
    date = time
  }
  else {
    if (typeof time === 'string' && /^[0-9]+$/.test(time)) {
      time = Number.parseInt(time)
    }
    else if (typeof time === 'string') {
      time = time
        .replace(new RegExp(/-/gm), '/')
        .replace('T', ' ')
        .replace(new RegExp(/\.[\d]{3}/gm), '')
    }
    if (typeof time === 'number' && time.toString().length === 10)
      time = time * 1000

    date = new Date(time)
  }
  const formatObj: Record<string, string> = {
    y: date.getFullYear(), // 年
    m: date.getMonth() + 1, // 月
    d: date.getDate(), // 日
    h: date.getHours(), // 时
    i: date.getMinutes(), // 分
    s: date.getSeconds(), // 秒
    a: date.getDay(), // 星期几
  }
  const time_str = format.replace(/{(y|m|d|h|i|s|a)+}/g, (result, key) => {
    let value = formatObj[key]
    // 注意：getDay()返回的是0表示星期天
    if (key === 'a')
      return ['日', '一', '二', '三', '四', '五', '六'][value]

    if (result.length > 0 && Number(value) < 10)
      value = `0${value}`

    return value || 0
  })
  return time_str
}

/**
 * @description trim函数
 * @param {string} str
 * @return {string}
 */
export function trim(str: string): string {
  return str.replace(/^\s+|\s+$/g, '') // 去除字符串两端的空格
}

/**
 * @description uuid的生成
 * @return {string}
 */
/**
 * @description 生成UUID
 * @return {string}
 */
export function getUUID(): string {
  const s: string[] = []
  const hexDigits = '0123456789abcdef'
  for (let i = 0; i < 36; i++) {
    s[i] = hexDigits[Math.floor(Math.random() * 0x10)]
  }
  s[14] = '4'
  s[19] = hexDigits[(parseInt(s[19], 16) & 0x3) | 0x8]
  s[8] = s[13] = s[18] = s[23] = '-'

  const uuid = s.join('')
  return uuid
}
// 38673f6b-bacc-4d9b-9330-dd97b7ae238f

/**
 * @description 千分位
 * @param {string | number} num
 * @return {void}
 */
export function addThousand(num: string | number): string {
  if (num)
    num = Number(num).toFixed(2)

  if ((!num && num !== 0) || num == 'NaN')
    return '--'
  const regForm = /(\d{1,3})(?=(\d{3})+(?:$|\.))/g
  num = num.toString().replace(regForm, '$1,')
  return num
}

/**
 * @description 大数值转换和保留n位有效数字
 * @param {number} num {number} digits
 * @return {string}
 */
export function numberFormatter(num: number, digits: number | undefined): string {
  const si = [
    { value: 1e13, symbol: '亿亿' },
    { value: 1e12, symbol: '万亿' },
    { value: 1e11, symbol: '千亿' },
    { value: 1e10, symbol: '百亿' },
    { value: 1e9, symbol: '十亿' },
    { value: 1e8, symbol: '亿' },
    { value: 1e7, symbol: '千万' },
    { value: 1e6, symbol: '百万' },
    { value: 1e5, symbol: '十万' },
    { value: 1e4, symbol: '万' },
    { value: 1e3, symbol: '千' },
  ]
  for (let i = 0; i < si.length; i++) {
    if (num >= si[i].value)
      return (num / si[i].value).toFixed(digits).replace(/\.0+$|(\.[0-9]*[1-9])0+$/, '$1') + si[i].symbol
  }
  return num.toString()
}

/**
 * @description 复制方法
 * @param {string} value 传入要复制的值
 * @return {string | MessageHandler}
 */
export const copy = (value: string): string | MessageHandler => {
  if (!value)
    return ElMessage.error('复制失败')

  const tag = document.createElement('textarea')
  tag.value = value
  document.body.appendChild(tag)
  tag.select()
  document.execCommand('copy')
  ElMessage.success('复制成功')
  tag.remove()
  return value
}

/**
 * @description 防抖
 * @return {function}
 * @param fn
 * @param delay
 * @param immediately
 */
export function debounce(fn, delay, immediately) {
  let timerID = -1;
  return function (...arg) {
    if (timerID < 0 && immediately) {
      fn.apply(this, arg);
      timerID = 1;
      return;
    }
    if (timerID > 0) {
      clearTimeout(timerID);
    }
    timerID = setTimeout(() => {
      console.log('arg', arg);
      fn.apply(this, arg);
    }, delay);
  };
}

/**
 * @description 节流
 * @param {number} timer
 * @return {function}
 */
export const throttle: (fn: (...args: unknown[]) => void, timer: number) => (...args: unknown[]) => void = (fn, timer = 0) => {
  let time: number | null = null
  return (...args: unknown[]) => {
    if (time)
      clearTimeout(time)
    time = setTimeout(() => {
      fn.apply(this, args)
    }, timer)
  }
}
```

### 9.2 storage

**utils/storage.js**

```js
/**
 * window.localStorage 浏览器永久缓存
 * @method set 设置永久缓存
 * @method get 获取永久缓存
 * @method remove 移除永久缓存
 * @method clear 移除全部永久缓存
 */
export const Local = {
  // 设置永久缓存
  set(key: string, val: any) {
    window.localStorage.setItem(key, JSON.stringify(val))
  },

  // 获取永久缓存
  get(key: string) {
    const json: any = window.localStorage.getItem(key)
    return JSON.parse(json)
  },

  // 移除永久缓存
  remove(key: string) {
    window.localStorage.removeItem(key)
  },

  // 移除全部永久缓存
  clear() {
    window.localStorage.clear()
  },
}

/**
 * window.sessionStorage 浏览器临时缓存
 * @method set 设置临时缓存
 * @method get 获取临时缓存
 * @method remove 移除临时缓存
 * @method clear 移除全部临时缓存
 */
export const Session = {
  // 设置临时缓存
  set(key: string, val: any) {
    window.sessionStorage.setItem(key, JSON.stringify(val))
  },

  // 获取临时缓存
  get(key: string) {
    const json: any = window.sessionStorage.getItem(key)
    return JSON.parse(json)
  },

  // 移除临时缓存
  remove(key: string) {
    window.sessionStorage.removeItem(key)
  },

  // 移除全部临时缓存
  clear() {
    window.sessionStorage.clear()
  },
}
```

### 9.3 iq(消息提示封装)

**iq.js**

```ts
/* 自行修改js和变量名 */

// 工具类提示信息
import { ElNotification, ElMessageBox, ElMessage } from "element-plus";

type MessageType = "info" | "success" | "error" | "warning";

/** 封装任意提示类型通知，默认info */
export function koiNotice(message: any, title = "温馨提示", duration = 2000, type: MessageType = "info", parseHtml = false) {
  ElNotification.closeAll();
  ElNotification({
    message,
    title,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示通知，默认success */
export function koiNoticeSuccess(
  message: any,
  title = "温馨提示",
  duration = 2000,
  type: MessageType = "success",
  parseHtml = false
) {
  ElNotification.closeAll();
  ElNotification({
    message,
    type,
    title,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示通知，默认error */
export function koiNoticeError(
  message: any,
  title = "温馨提示",
  duration = 2000,
  type: MessageType = "error",
  parseHtml = false
) {
  ElNotification.closeAll();
  ElNotification({
    message,
    type,
    title,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示通知，默认warning */
export function koiNoticeWarning(
  message: any,
  title = "温馨提示",
  duration = 2000,
  type: MessageType = "warning",
  parseHtml = false
) {
  ElNotification.closeAll();
  ElNotification({
    message,
    title,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示通知，默认info */
export function koiNoticeInfo(message: any, title = "温馨提示", duration = 2000, type: MessageType = "info", parseHtml = false) {
  ElNotification.closeAll();
  ElNotification({
    message,
    title,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}

/** 封装提示信息，默认info */
export function koiMsg(message: any, duration = 2000, type: MessageType = "info", parseHtml = false) {
  ElMessage.closeAll();
  ElMessage({
    message,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示信息，默认success */
export function koiMsgSuccess(message: any, duration = 2000, type: MessageType = "success", parseHtml = false) {
  ElMessage.closeAll();
  ElMessage({
    message,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示信息，默认error */
export function koiMsgError(message: any, duration = 2000, type: MessageType = "error", parseHtml = false) {
  ElMessage.closeAll();
  ElMessage({
    message,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示信息，默认warning */
export function koiMsgWarning(message: any, duration = 2000, type: MessageType = "warning", parseHtml = false) {
  ElMessage.closeAll();
  ElMessage({
    message,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}
/** 封装提示信息，默认info */
export function koiMsgInfo(message: any, duration = 2000, type: MessageType = "info", parseHtml = false) {
  ElMessage.closeAll();
  ElMessage({
    message,
    type,
    duration: duration,
    showClose: true,
    dangerouslyUseHTMLString: parseHtml
  });
}

/** 封装确认信息，默认warning */
export function koiMsgBox(
  message: any = "您确定进行关闭么？",
  title: string = "温馨提示：",
  confirmButtonText: string = "确定",
  cancelButtonText: string = "取消",
  type: string = "warning"
): Promise<boolean> {
  return new Promise((resolve, reject) => {
    ElMessageBox.confirm(
      message as any,
      title as any,
      {
        confirmButtonText,
        cancelButtonText,
        type,
        draggable: true,
        dangerouslyUseHTMLString: true
      } as any
    )
      .then(() => {
        resolve(true);
      })
      .catch(() => {
        reject(false);
      });
  });
}

/** 封装确认信息，默认warning  */
export function koiMsgBoxHtml(
  message: any = `<p style="color: teal">您确定进行关闭么？</p>`,
  title: string = "温馨提示：",
  confirmButtonText: string = "确定",
  cancelButtonText: string = "取消",
  type: string = "warning"
): Promise<boolean> {
  return new Promise((resolve, reject) => {
    ElMessageBox.confirm(
      message as any,
      title as any,
      {
        confirmButtonText,
        cancelButtonText,
        type,
        draggable: true,
        dangerouslyUseHTMLString: true
      } as any
    )
      .then(() => {
        resolve(true);
      })
      .catch(() => {
        reject(false);
      });
  });
}

/** Prompt 类型的消息框 */
export function koiMsgBoxPrompt(
  message: any = "请输入需要修改的数据？",
  title: string = "温馨提示：",
  confirmButtonText: string = "确定",
  cancelButtonText: string = "取消",
  type: string = "info",
  inputPattern: string = "",
  inputErrorMessage: string = "无效输入"
): Promise<boolean> {
  return new Promise((resolve, reject) => {
    ElMessageBox.prompt(
      message as any,
      title as any,
      {
        confirmButtonText: confirmButtonText,
        cancelButtonText: cancelButtonText,
        type,
        inputPattern: inputPattern,
        inputErrorMessage: inputErrorMessage,
        draggable: true
      } as any
    )
      .then((res: any) => {
        // 返回值获取通过[res.value]
        resolve(res);
      })
      .catch(() => {
        reject(false);
      });
  });
}

/** Alert 类型的消息框 */
export function koiMsgBoxAlert(
  message: any = "请输入需要修改的数据？",
  title: string = "温馨提示：",
  confirmButtonText: string = "确定",
  type: string = "info"
): Promise<boolean> {
  return new Promise((resolve, reject) => {
    ElMessageBox.alert(
      message as any,
      title as any,
      {
        confirmButtonText: confirmButtonText,
        type,
        draggable: true
      } as any
    )
      .then(() => {
        // 返回值获取通过[res.value]
        resolve(true);
      })
      .catch(() => {
        reject(false);
      });
  });
}
```

## 10. 使用pinia

### 10.1 global

**modules/global.js**

```js
// 定义全局主题配置小仓库（选择式Api写法）
import { defineStore } from "pinia";
import { PINIA_PREFIX, DEFAULT_THEME } from "@/config/index.ts";

// defineStore方法执行会返回一个函数，函数的作用就是让组件可以获取到仓库数据
const globalStore = defineStore("global", {
  // 开启数据持久化
  persist: {
    // enabled: true, // true 表示开启持久化保存
    key: PINIA_PREFIX + "global", // 默认会以 store 的 id 作为 key
    storage: localStorage
  },
  // 存储数据state
  state: () => {
    return {
      // 是否全屏
      isFullScreen: false,
      // 是否折叠菜单
      isCollapse: false,
      // 菜单展开宽度[默认：220px]
      menuWidth: 220,
      // 默认关闭黑暗模式
      isDark: false,
      // ElementPlus 尺寸大小
      dimension: "default",
      // 当前页面是否全屏
      maximize: false,
      // 当前系统语言[默认中文]
      language: "zh",
      // 选择主题[默认兔子坦克形态]
      themeColor: DEFAULT_THEME,
      // 布局模式 (纵向：vertical | 经典：classic | 横向：horizontal | 分栏：column)
      layout: "vertical",
      // 路由动画
      transition: "fade-default",
      // 菜单是否可展开单个[默认：true仅仅一个]
      uniqueOpened: true,
      // 灰色模式
      isGrey: false,
      // 色弱模式
      isWeak: false,
      // 侧边栏反转
      asideInverted: false,
      // 头部反转
      headerInverted: false
    };
  },
  actions: {
    // 设置当前global.ts所有参数值
    setGlobalState(...args: any) {
      this.$patch({ [args[0]]: args[1] });
    },
    // 该函数没有上下文数据，所以获取state中的变量需要使用this
    setCollapse(value: boolean) {
      this.isCollapse = !value;
      return this.isCollapse;
    },
    // 设置左侧菜单宽度
    setMenuWidth(value: number) {
      this.menuWidth = value;
      return this.menuWidth;
    },
    // 设置ElementPlus尺寸
    setDimension(value: string) {
      this.dimension = value;
    }
  },
  // 计算属性，和vuex是使用一样，getters里面不是方法，是计算返回的结果值
  getters: {}
});

// 对外暴露方法
export default globalStore;
```

## 11. layout布局

11.2 整Layout

## 13. hooks



## 14. 组件封装

## 15. 安装动画

官网：`https://animate.style/`

```bash
npm install animate.css --save
```

16.解决chrome警告

```bash
// 安装   
npm install default-passive-events -S
// 在main.js引入
// 添加事件管理者'passive'，来阻止'touchstart'事件，让页面更加流畅。 解决chrome下的warning问题
import 'default-passive-events';
```

## 16. 版本管理

standard-version参考：

`https://juejin.cn/post/7356434494511792164`

`https://juejin.cn/post/7020289124993073189`

```json
"scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "release": "standard-version",
    "release:first": "standard-version --first-release", // 首次发布，不升级版本号
    "release-major": "standard-version --release-as major"
},
```

```bash
npm i --save-dev standard-version
或者
npm install -D standard-version


```

**release-it**

```bash
npm install -D release-it @release-it/conventional-changelog
```

**根目录新建.release-it.json**

```json
{
  "plugins": {
    "@release-it/conventional-changelog": {
      "header": "# 变更日志", // changelog中显示的头部信息，
      // 自定义提交类型
      "preset": { // 应用预设
        "name": "conventionalcommits",
        "types": [
          // "hidden": true 隐藏
           { "type": "feat", "section": "✨ Features | 新功能" },
           { "type": "fix", "section": "🐛 Bug Fixes | Bug 修复" },
           { "type": "chore", "section": "🎫 Chores | 其他更新" },
           { "type": "docs", "section": "📝 Documentation | 文档" },
           { "type": "style", "section": "💄 Styles | 风格" },
           { "type": "refactor", "section": "♻ Code Refactoring | 代码重构" },
           { "type": "perf", "section": "⚡ Performance Improvements | 性能优化" },
           { "type": "test", "section": "✅ Tests | 测试" },
           { "type": "revert", "section": "⏪ Reverts | 回退" },
           { "type": "build", "section": "👷‍ Build System | 构建" },
           { "type": "ci", "section": "🔧 Continuous Integration | CI 配置" },
           { "type": "config", "section": "🔨 CONFIG | 配置" }
        ]
      },
      "infile": "CHANGELOG.md", // 生成变更日志的名字
      // 笔者希望自己选择 bump 的策略，而不是按照推荐的策略，因此将此选项打开
      // 是否自己命名版本号，true是自己选
      "ignoreRecommendedBump": false, 
      // 笔者希望发布的版本号必须是 strict-semver 的版本号，因此将此选项打开
      "strictSemVer": true
    }
  },
  // 插件会自动生成tag，我们需要自定义一下生成tag时的提交信息。在配置项中加入下面的配置，来完成提交信息的自定义：
  "git": {
    "commitMessage": "chore: Release v${version}" // 更新版本时 git需要提交package.json的变更，
  },
  "github": {
    "release": true, // 是否开启git仓库release
    "draft": false
  },
  "npm": {
	"publish": false // 是否需要在npm发布
  },
  "hooks": {
    "after:bump": "echo 更新版本成功" // hook在提升版本后执行该hook
  }
}
```

**或者选择在package.json中配置**

```json
{
  "name": "my-package",
  "devDependencies": {
    "release-it": "*"
  },
  "release-it": {
    "github": {
      "release": true
    }
  }
}
```

**配置脚本**

```json
"scripts": {
	"release": "release-it"
},
```

- 查看changelog

```
npx release-it --changelog
```

- 查看下一个该发布的版本号

```
npx release-it --release-version
```
