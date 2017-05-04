# 不用手脚架vue-cli创建项目 ##

## 1、项目目录结构 ##
    |-index.html  入口html文件
    |-main.js 程序入口文件，用于加载各种组件
    |-App.vue  页面入口文件
    |-webpack.config.js  webpack配置文件
    |-package.json  项目依赖工具文件
        |-npm install init --yes

## 2、配置webpack.config.js 文件 ##
```javeScript
module.exports = {
    entry:'./main.js',//入口
    output:{//文件输出
        path:__dirname,
        filename:'build.js'//模板
    },
    module:{
        rules:[
            {//解析vue
                test:/\.vue$/,
                loader:'vue-loader'
            },
            {//解析es6
                test:/\.js$/,
                loader:'babel-loader',
                exclude:/node_modules/
            }
        ]
    }
}
</script>
```

## 3、webpack 准备工作 ##

    安装
    npm install webpack webpack-dev-server --save-dev


## 4、package.json文件配置 ##

    "dev": "webpack-dev-server --inline --hot"

    解析：
    webpack-dev-server //开始本地服务器
    --inline //刷新
    --hot //热加载


## 5、 各种loader安装 ##

    （1） 解析.vue结尾文件
        npm install vue-loader@8.5.4  --save-dev
    （2） 解析App.vue文件中的template script style的loader
        npm install
            vue-html-loader  ---html
            vue-hot-reload-api@1.3.2  ---js
            css-loader vue-style-loader ---css
            记得最后尾加上 --save-dev
    （3）解析es6语法的loader
        npm install
            babel-loader
            babel-core
            babel-plugin-transform-runtime
            babel-preset-es2015
            babel-runtime
            记得最后尾加上 --save-dev

## 6、 安装vue ##
    npm install vue@1.0.28 --save


## 7、 书写index.html文件内容
```javeScript
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
        <div id="box">
            <app></app>
        </div>
        <script src="build.js"></script>
    </body>
    </html>
</script>
```

## 8、 App.vue文件内容
```javeScript
<template>
    <h3>{{msg}}</h3>
</template>
<script>
    export default {
        data:function(){
            return {
                msg:"欢迎一起分享vue!"
            }
        }
    }
</script>
<style>
</style>
</script>
```

    说明：
    es6语法糖
    1、 导出模块
        export default {}  ===  new Vue({})
    2、 引入模块
        import 模块名 from 模块地址

## 9、 书写main.js文件内容

```javeScript
import Vue from "vue"
import App from "./App.vue"
new Vue({
    el:"#box",
    components:{
        App
    }
})
</script>
```

## 10、 运行 ##

    npm run dev
