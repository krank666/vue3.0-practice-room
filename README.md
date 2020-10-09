# vue3.0-practice-room

vue3.0学习仓，记录，爬坑，实践，分享

## 一、使用vue-cli4.5+安装VUE3.0

1. 首先需要按照原始搭建模式下载vue脚手架

> npm install -g @vue/cli

> vue create vue3.0-practice-room

2. 选择安装3.0版本vue（vue-cli，4.5版本已有此选项，往前版本未测试）

> 在Choose a version of Vue.js that you want to start the project with时候选择3.x


## 二、创建我的第一个vue3.0文件

在项目创建完成后，脚手架已经帮我们生成了基础目录和几个示例代码，目录结构和2.0非常相似
我们在views目录下创建第一个页面 MyPage.vue，看起来和vue2.0非常像

``` vue
<template>
  <div class="myPage">
　　   <h1>欢迎来到vue3的世界</h1>
  </div>
</template>

<script>
 export default {
 }
</script>

<style lang="less" scoped>
.myPage {
  color: blue;
}
</style>

```

然后我们去路由里面添加它，这里注意和vue2的区别了

``` js
import {
    createRouter,
    createWebHistory
} from 'vue-router'
import Home from '../views/Home.vue'

const routes = [{
        path: '/',
        name: 'Home',
        component: Home
    },
    {
        path: '/MyPage',
        name: 'MyPage',
        // route level code-splitting
        // this generates a separate chunk (about.[hash].js) for this route
        // which is lazy-loaded when the route is visited.
        component: () => import( /* webpackChunkName: "about" */ '../views/MyPage.vue')
    }
]

const router = createRouter({
    history: createWebHistory(),
    routes
})

export default router
```

我们清理掉About相关代码，不去理会

这里的路由不再是Vue.use这种模式，而是变成了

createRouter

createWebHistory 这两个函数

函数内部作用我们后期拆解，这里不做过多介绍，我们可以看到他们一个是创建了基础路由，一个创建了路由所需的配置，createWebHistory接收一个参数为项目路由的baseUrl, 我们这里不传

不要忘记修改App.vue根文件里面添加上我们刚才写的路由，一样的把About清理掉

``` vue
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/MyPage">MyPage</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

```

运行 npm run serve 查看效果了