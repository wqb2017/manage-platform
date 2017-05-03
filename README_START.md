# 正式开始 #

## 构建项目框架 ##

### 1、安装vue
    $ cnpm install vue@2.1.6
    # 全局安装 vue-cli
    $ cnpm install --global vue-cli
    # 创建一个基于 webpack 模板的新项目my-project
    $ vue init webpack my-project
    # 进入项目目录
    $ cd my-project
    # 安装依赖，走你
    $ cnpm install
    # 运行项目
    $ cnpm run dev
### 2、运行项目之后，出现欢迎界面为成功搭建项目

### 3、说明项目结构，目录

### 4、搭建项目的首页

项目首页由顶部栏，左侧导航栏，中间内容区构成

4.1 安装element-ui

$ cnpm i element-ui@1.0.9

建议固定vue和element-ui的版本，避免将来版本升级后产生冲突

4.2 引入element-ui

在app.vue引入element-ui，然后就可以在其他任何页面中使用了

 import Element from 'element-ui'
 import 'element-ui/lib/theme-default/index.css'
 Vue.use(Element)

4.3 使用element-ui

```JavaScript
<template>
      <div id="app">
        <!-- 头部导航 -->
        <header class="header">
        <el-row>
            <el-col :span="24">
              <el-menu default-active="5" class="el-menu-demo" mode="horizontal" @select="">
                <el-menu-item index="1">高级插件</el-menu-item>
                <el-menu-item index="2">在线商城</el-menu-item>
                <el-menu-item index="3">客户管理</el-menu-item>
                <el-menu-item index="4">系统设置</el-menu-item>
                <el-menu-item index="5">活动发布</el-menu-item>
              </el-menu>
            </el-col>
        </el-row>
        </header>
        <div style="position: relative;height: 60px;width: 100%;"></div>

        <main>
              <!-- 左侧导航 -->
            <div class="main-left">
              <el-menu default-active="/activePublic" class="el-menu-vertical-demo" :router="true">
                <el-menu-item index="/activePublic" :class="{'isActive': active}">活动发布</el-menu-item>
                <el-menu-item index="/activeManage" :class="{'isActive': !active}">活动管理</el-menu-item>
              </el-menu>
            </div>

              <!-- 右侧主内容区 -->
              <div  class="main-right" >

              </div>
        </main>
      </div>
    </template>

    <script>
    import Vue from 'vue'
    import Element from 'element-ui'
    import 'element-ui/lib/theme-default/index.css'

    Vue.use(Element)

    export default {
      name: 'app',
      data: function (){
        return {
          active:true
        }
      }
    }
    </script>

    <style>
      body{margin: 0;}
    #app {
      min-width: 1200px;
      margin: 0 auto;
      font-family: "Helvetica Neue","PingFang SC",Arial,sans-serif;
    }
    /* 头部导航 */
    header{z-index: 1000;min-width: 1200px;transition: all 0.5s ease;  border-top: solid 4px #3091F2;  background-color: #fff;  box-shadow: 0 2px 4px 0 rgba(0,0,0,.12),0 0 6px 0 rgba(0,0,0,.04);  }
    header.header-fixed{position: fixed;top: 0;left: 0;right: 0;}
    header .el-menu-demo{padding-left: 300px!important;}

    /* 主内容区 */
      main{    display: -webkit-box;  display: -ms-flexbox;  display: flex;  min-height: 800px;  border: solid 40px #E9ECF1;  background-color: #FCFCFC;  }
      main .main-left{text-align: center;width: 200px;float: left;}
      main .main-right{-webkit-box-flex: 1;  -ms-flex: 1;  flex: 1;  background-color: #fff; padding: 50px 70px; }
      main .el-menu{background-color: transparent!important;}
    </style>
</script>
```

4.4 预览项目 npm run dev

5、 引入路由工具vue-router，切换视图

5.1 安装vue-router
cnpm install vue-router --save-dev

5.2 使用vue-router  main.js

```JavaScript
    // 0. 如果使用模块化机制编程，導入Vue和VueRouter，要调用 Vue.use(VueRouter)
    // 1. 定义（路由）组件。
    // 可以从其他文件 import 进来
//    const Foo = { template: '<div>foo</div>' }
//    const Bar = { template: '<div>bar</div>' }

    // 2. 定义路由
    // 每个路由应该映射一个组件。 其中"component" 可以是
    // 通过 Vue.extend() 创建的组件构造器，
    // 或者，只是一个组件配置对象。
    // 我们晚点再讨论嵌套路由。
    const routes = [
        { path: '/foo', component: Foo },
        { path: '/bar', component: Bar }
    ]
    // 3. 创建 router 实例，然后传 `routes` 配置
    // 你还可以传别的配置参数, 不过先这么简单着吧。
    const router = new VueRouter({
        routes // （缩写）相当于 routes: routes
    })
    // 4. 创建和挂载根实例。
    // 记得要通过 router 配置参数注入路由，
    // 从而让整个应用都有路由功能
    const app = new Vue({
        router
    }).$mount('#app')
    // 现在，应用已经启动了！
</script>
```

5.3 配置路由

```JavaScript
// 引入组件
import activePublic from './page/activePublic/index.vue'

export default [
   {
        // 配置路由，当路径为'/activePublic',使用组件activePublic
        path:'/activePublic',component:activePublic,
  }
]
</script>
```

5.4 使用路由 app.vue

```JavaScript
<template>
  <div id="app">
    <!-- 头部导航 -->
    ...

    <main>
          <!-- 左侧导航 -->
        <div class="main-left">
            ...
        </div>

          <!-- 右侧主内容区 -->
          <div  class="main-right" >
              <!-- 视图 -->
              <router-view class="view"></router-view>
          </div>
    </main>
  </div>
</template>
</script>
```

6、 在页面随便写点东西，测试一下，路由是否配置成功

```JavaScript
<template>
    <div class="activePublic ">

      <!-- element步骤组件 -->
      <el-steps :space="200" :active="step" class="step">
        <el-step title="活动信息" description=""></el-step>
        <el-step title="报名签到" description=""></el-step>
        <el-step title="分享设置" description=""></el-step>
        <el-step title="个性设置" description=""></el-step>
      </el-steps>
</template>
</script>
```

7、 配置二级路由

```JavaScript
import activePublic from './page/activePublic/index.vue'
<!-- 引入子页面 -->
import step1 from './page/activePublic/step1.vue'
import step2 from './page/activePublic/step2.vue'
import step3 from './page/activePublic/step3.vue'
import step4 from './page/activePublic/step4.vue'
export default [
  {
    path:'/activePublic',component:activePublic,
    // 配置子路由
    children:[
       // 路径为'/activePublic'，使用组件step1
      { path: ''      , component: step1  },
       // 路径为'/activePublic/step1'，使用组件step1
      { path: 'step1', component: step1  },
      // 路径为'/activePublic/step2'，使用组件step2
      { path: 'step2', component: step2  },
      { path: 'step3', component: step3  },
      { path: 'step4', component: step4  }
    ]
  }
]
</script>
```
