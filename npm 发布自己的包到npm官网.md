# npm 发布自己的包到npm官网
  参考于： https://zhuanlan.zhihu.com/p/459284053
  准备工作
 1. https://www.npmjs.com/  注册自己的账号 记录下来
 2. 用npm create 创建一个最简单的项目

  组件封装
    新建package文件夹
    
    目录结构
    ```
    src
      assets
      components
      package
        pig-button
          index.vue
        pig-input
          index.vue
    App.vue
    main.js
    ```
    
 1.1编写组件代码
这里我们就以pig-button组件为例，任意编写一点代码，代码如下：
```
<template>
  <div>
    <button>我是测试按钮</button>
  </div>
</template>
<script>
export default {
  name: "pig-button", //组件名
};
</script>
<style scoped>
button {
  width: 100px;
}
</style>
```    
 1.2 使用Vue插件模式
   这一步是封装组件中的重点，用到了Vue提供的一个公开方法：install。这个方法会在你使用Vue.use(plugin)时被调用，这样使得我们的插件注册到了全局，在子组件的任何地方都可以使用。
在<span style='color:red'>package</span>目录下新建index.js文件，代码如下：
```
//package/index.js
import PigButton from "../package/pig-button/index.vue"; // 引入封装好的组件
const coms = [PigButton]; // 将来如果有其它组件,都可以写到这个数组里

// 批量组件注册
const install = function (Vue) {
  coms.forEach((com) => {
    Vue.component(com.name, com);
  });
};

export default install; // 这个方法以后再使用的时候可以被use调用
```

1.3 组件打包 （必须有）
   最外层  修改我们项目得package.json文件，配置打包命令：
   在scripts 下面添加
   
    "package": "vue-cli-service build --target lib ./src/package/index.js --name pig-ui --dest pig-ui"
    
1.4 打包
   npm run  package
   打包执行完成后我们项目目录下就会多出一个pig-ui文件夹，存放的是打包后的文件。

1.5 发布到npm
   在最外层 pig-ui 下面 执行 npm init -y  生成新的package.json 文件
   其中mian:"*.js" 为入口文件 很重要！！
   
   执行npm publish --access public    //发布公有
   
1.6 新项目中应用 刚才发布的包
```
npm install pig-ui-test // 安装包

然后在main.js引用注册，代码如下：

import PigUi from "pig-ui-test";
import "../node_modules/pig-ui-test/pig-ui.css";  //引用css
Vue.use(PigUi);

因为当时导出的是 pig-button     模板中使用
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <pig-button></pig-button>
  </div>
</template>
```



       
       

   
              
 


  
  
  

