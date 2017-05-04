## 构建项目框架 ##

### 1、手动创建项目框架

    项目结构
    vue-project
        |-index.html 入口html文件
        |-main.js 程序入口文件，加载各种公共组件
        |-App.vue 页面入口文件
        |-webpack.config.js webpack配置文件
        |-package.json 项目及工具的依赖配置文件

   所需loader
       vue-loader  vue-style-loader vue-html-loader
       webpack  //npm install webpack webpack-dev-server --save-dev
       babel //npm babel-loader babel-core babel-preset-es2015

   安装vue
        vue //npm install vue


   配置webpack.config.js文件
   ```JavaScript
   module.exports = {
       entry: "./main.js",
       output: {
           path: __dirname + "/dist",
           filename: "bundle.js"
       },
       module:{
           rules: [
               {
                   test: /\.vue$/,
                   loader: 'vue-loader'
               },
               {
                   test: /\.js$/,
                   loader: 'babel-loader',
               }
           ]
       }
   };
   </script>
   ```

   配置package
   "dev": "webpack-dev-server --inline --hot";

   运行dev
        npm run dev

   访问 localhost:8082

### 常用网址 ####

1、 webpack http://webpack.github.io/docs/

2、 npmjs https://www.npmjs.com/

