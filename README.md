# vant

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

### 技术选型

Vue+VueX+Vant+Axios+Node.js+Expresss+MySQL

### 版本管理

自动化部署工具 git+码云 Gitee

### 业务功能

后端
接口采用 restful 原则设计，方便统一请求业务功能
接口文件按功能划分，方便阅读维护
服务器端口 3000
接口 restful 设计原则
sql 语句要防止 sql 注入
cors(跨源资源共享)
session
错误处理 404 500

前端
懒加载
短信验证登录
购物车
图片预览+上传
点赞、评论
轮播图
级联菜单
下拉刷新上拉加载
运用路由守卫进行 登录拦截

### 代码实现注意事项

工具最好都重新安装一次
vscode，有些快捷键以及插件需要自己重新配置，
安装的插件尽量选择合适自己的，插件之间的配置，以及系统的配置会有冲突
工具尽量更新到最新的版本
例如 git 的命令语义更清晰且简洁，vuecli 搭建的项目结构更简洁明了
工具的配置尽量优化
例如浏览器的地址栏的默认搜索引擎
文件夹以及路由命名用小写字母
路由命名规则，可以参考文件夹目录路径
对于文件的删除要弄清前因后果才可以操作，建议尽量不要删除文件
代码注释要充分
代码缩进统一 2 个字符
安装格式化插件 Prettier - Code formatter

默认布局规则
主题色选定
字体大小 rem
页面内边距 5px
板块之间的外边距 10px

### 项目结构

```shell
│  .gitignore Git忽略提交
│  babel.config.js
│  package-lock.json 第三方包版本锁定文件
│  package.json 包描述文件
│  README.md 项目说明文档
│  vue.config.js vue-cli配置文件
│
├─node_modules 保存当前项目本地安装的模块/包
│
├─public 专门保存不需要编译的静态文件的目录
│  │  favicon.ico
│  │  index.html 唯一完成的HTML页面
│  │
│  └─img 图片文件夹
│
└─src  保存所有咱们自己编写的需要打包和编译的代码
    │  App.vue 根组件 <div id="app"></div>
    │  main.js 入口函数 new Vue({})
    │
    ├─assets
    │  └─api 封装函数的文件夹，例如axios
    │
    ├─components 放所有除页面组件之外的一切子组件或全局组件
    │      Swiper.vue
    │
    ├─router 前端路由
    │      index.js
    │
    ├─store
    │      index.js
    │
    └─views 保存所有页面组件
            Details.vue
            Index.vue
```

### 配置懒加载

- 项目本地安装

```shell
npm i @babel/plugin-syntax-dynamic-import -D
```

- 在项目根目录，添加 vue.config.js 配置文件

```js
module.exports = {
  chainWebpack: config => {
    // 删除编译后的独立js文件上的预获取操作
    config.plugins.delete("prefetch");
  }
};
```

### vant

```shell
npm i vant
```

```shell
npm i babel-plugin-import -D
```

babel.config.js 配置

```js
module.exports = {
  plugins: [
    [
      "import",
      {
        libraryName: "vant",
        libraryDirectory: "es",
        style: true
      },
      "vant"
    ]
  ]
};
```

assets/vant/vant-ui.js 按需引入组件

```js
import Vue from "vue";
import {
  AddressEdit,
  AddressList,
  Area,
  Button,
  Card,
  Cell,
  CellGroup,
  Checkbox,
  CheckboxGroup,
  Col,
  Dialog,
  Divider,
  Field,
  Grid,
  GridItem,
  Icon,
  Image,
  ImagePreview,
  Lazyload,
  List,
  NavBar,
  Panel,
  PullRefresh,
  Row,
  Stepper,
  SubmitBar,
  Swipe,
  SwipeCell,
  SwipeItem,
  Tabbar,
  TabbarItem,
  Toast,
  Uploader
} from "vant";

Vue.use(AddressEdit);
Vue.use(AddressList);
Vue.use(Area);
Vue.use(Button);
Vue.use(Card);
Vue.use(Cell);
Vue.use(CellGroup);
Vue.use(Checkbox);
Vue.use(CheckboxGroup);
Vue.use(Col);
Vue.use(Dialog);
Vue.use(Divider);
Vue.use(Field);
Vue.use(Grid);
Vue.use(GridItem);
Vue.use(Icon);
Vue.use(Image);
Vue.use(ImagePreview);
Vue.use(Lazyload);
Vue.use(List);
Vue.use(NavBar);
Vue.use(Panel);
Vue.use(PullRefresh);
Vue.use(Row);
Vue.use(Stepper);
Vue.use(SubmitBar);
Vue.use(Swipe);
Vue.use(SwipeCell);
Vue.use(SwipeItem);
Vue.use(Tabbar);
Vue.use(TabbarItem);
Vue.use(Toast);
Vue.use(Uploader);
```

main.js 配置

```js
import "./assets/vant/vant-ui";
```

### axios

```shell
npm i axios
```

main.js 配置

```js
// 导入axios第三方ajax模块
import axios from "axios";
// 配置axios基础路径
axios.defaults.baseURL = "http://127.0.0.1:3000";
// 配置axios保存session信息
axios.defaults.withCredentials = true;
// 将axios注册到vue实例中，由于axios不支持use，所以将实例添加到vue原型
Vue.prototype.axios = axios;
```

assets/api/home.js

```js
import axios from "axios";
// 模块都是单例模式：整个内存中只有一个axios，只不过被导出引用着使用而已
// 所以这里import的axios，就是main.js中配置的axios对象

// export function getBanner() {
//   return new Promise((resolve, reject) => {
//     axios
//       .get("/user/v12/searchuser/root")
//       .then(result => {
//         resolve(result.data);
//       })
//       .catch(err => {
//         reject(err);
//       });
//   });
// }

export async function getBanner() {
  try {
    const result = await axios.get("http://localhost:3000/carousel");
    return result.data;
  } catch (err) {
    console.log(err);
    console.log("请求出错了");
  }
}
```

```js
import { getBanner } from "../../assets/api/home.js";
//      对象解构        模块对象，其中包含getIndex()
import swiper from "../../components/Swiper";
export default {
  data() {
    return {
      bannerlist: [{ imgsrc: "" }]
    };
  },
  created() {
    getBanner().then(res => (this.bannerlist = res));
  },
  methods: {},
  components: {
    swiper
  }
};
```

### address

```js
const address = [
  {
    id: 1,
    uid: 1,
    name: "jack",
    tel: "13000000000",
    province: "浙江省",
    city: "杭州市",
    county: "西湖区",
    addressDetail: "文三路 138 号东方通信大厦 7 楼 501 室路",
    address: "浙江省杭州市西湖区文三路 138 号东方通信大厦 7 楼 501 室",
    areaCode: "360103",
    postalCode: "360103",
    isDefault: true,
    href: "/home",
    isDelete: 0
  },
  {
    id: 2,
    uid: 1,
    name: "lam",
    tel: "13510740753",
    province: "北京市",
    city: "北京市",
    county: "东城区",
    addressDetail: "万寿路",
    address: "北京市东城区万寿路",
    areaCode: "110101",
    postalCode: "110101",
    isDefault: false,
    href: "/home",
    isDelete: 0
  },
  {
    id: 3,
    uid: 1,
    name: "lucy",
    tel: "13511234563",
    province: "广东省",
    city: "深圳市",
    county: "龙华区",
    addressDetail: "嘉熙业",
    address: "广东省深圳市龙华区嘉熙业",
    areaCode: "440309",
    postalCode: "440309",
    isDefault: false,
    href: "/home",
    isDelete: 0
  }
];
```

### vue-router 中 name 的用法

```js
export default new Router({
  routes: [
    {
      path: "/",
      name: "HelloWorld",
      component: HelloWorld
    },
    {
      path: "/textInner",
      name: "textInner",
      component: text
    },
    {
      path: "/text/:id",
      component: param
    }
  ]
});
```

第一种用法：通过 name 属性，为一个页面中不同的 router-view 渲染不同的组件，如：将上面代码的 HelloWorld 渲染在 name 为 HelloWorld 的 router-view 中，将 textInner 渲染在 name 为 textInner 的 router-view 中，不设置 name 的将为默认的渲染组件。

```html
<template>
  <div id="app">
    <router-view></router-view>
    <!-- 将渲染HelloWorld组件 -->
    <router-view name="HelloWorld"></router-view>
    <!-- 将渲染textInner组件 -->
    <router-view name="textInner"></router-view>
  </div>
</template>
```

第二种用法：使用\$router.name 获取组件 name 值

```html
<template>
  <div id="app">
    <p>{{ $route.name }}</p>
    <!-- 可以获取到渲染进来的组件的name值;点击谁的路由就显示路由的name值 -->
    <router-view></router-view>
  </div>
</template>
```

第三种用法：页面渲染时传递参数

```html
<template>
  <div id="app">
    <!-- 向name为helloWorld的组件传参数id，值为11 -->
    <router-link :to="{name:'helloWorld', params:{id: '11'}}">
      hello
    </router-link>
    <router-view></router-view>
  </div>
</template>
```

### 封装组件 panel

html 结构

```html
<div class="panel">
  <div class="title"></div>
  <div class="item"></div>
</div>
```

在项目目录 assets 下新建文件夹 css，在 css 文件夹里创建 panel.css 文件，样式结构如下

```css
.panel {
}
.panel .title {
}
.panel .item {
}
```

### cart

数据结构

```js
var cart = {
  id: 1,
  uid: 1, // shoppingcart uid 与 user id 外键关联
  name: "a",
  number: 1,
  price: 2.0,
  desc: "Apple iPhone 8 Plus (A1864) 64GB 金色 移动联通电信4G手机其它内存",
  title: "apple",
  thumb: "https://img.yzcdn.cn/vant/t-thirt.jpg",
  ischecked: 0,
  isdeleted: 0 // 软删除标记
};
```

接口
查询：根据 uid 和条件 isdeleted=0 查询购物车数据
修改：根据 id 修改商品数量 number
删除：考虑到批量操作，删除的接口可以用 in 条件设计
插入

### product

```js
const product = [
  {
    id: 1,
    proName: "144757c三星标黑色", // 商品名称
    proDesc: "指南针运动 NIKE HYPERSHIFT篮球鞋 844392-010-607-164-017现货", // 商品描述
    market_price: 999, // 市场价
    sell_price: 699, // 销售价
    statu: 1, // 是否上架
    updateTime: "2017-01-05 00:28:29", // 上架时间
    stock: 500, // 库存
    isDelete: 0,
    src: "/img/1.jpg", // 图片
    msrc: "/img/1-small.jpg", // 小图
    click: 15 // 点击数
  }
];
```

## 难点

前后台接口对应传递的数据不一样
前端 axios 请求传递的参数以及后端接收请求 req.body 里的 key 不一致， 需要给对象换 key 值/用到对象结构

用 vue 框架开发，转变编程思想，操作数据，对数组的函数应用很多，例如 reduce filter map some every forEach 等

修改组件库的默认样式不成功，原因就是组件中 style 的 scoped 属性对样式有限制，去掉即可

涉及第三方的接口，短信验证，支付，需要先理清客户端、服务端、第三方，三者之间请求响应的关系，参考其官方文档，SDK 的配置、通知验签，写出合适的接口

路由守卫 & token axios 拦截器 短信验证 支付数据 axios 请求时机 部署服务器

站在用户的角度考虑，改善用户体验，删除了繁琐的密码登录，减少无畏的记忆，只要用手机号码就可以登录，如果是新用户首次登录，即视为注册，输入验证码后完成注册

\$refs 的使用
