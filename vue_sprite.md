# vue-cli3 使用精灵图

## 1  创建spriteDetail文件夹

在assets目录下创建spriteDetail文件夹用于存放图片。将原来的logo.png文件移动到spriteDetail文件夹下。再增加一个图标trainning.png。如下图的文件结构所示：

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/sprite/docStru.png)


## 2  安装插件

```
npm i webpack-spritesmith -D
```

### 在vue.config.js文件中修改配置。增加以下代码

```
const path = require('path');
const SpritesmithPlugin = require("webpack-spritesmith");

```

### 在vue.config.js中增加样式处理模板

```
// 雪碧图样式处理模板
let templateFunction = function(data) {
  let shared = ".icon { display:inline-block; background-image: url(I); background-size:WSMpx HSMpx; }"
    .replace("I", data.sprites[0].image)
    .replace("WSM", data.spritesheet.width)
    .replace("HSM", data.spritesheet.height);

  let perSprite = data.sprites
    .map(function(sprite) {
      return ".icon-N { width: Wpx; height: Hpx; background-position: Xpx Ypx; }"
        .replace("N", sprite.name)
        .replace("W", sprite.width)
        .replace("H", sprite.height)
        .replace("X", sprite.offset_x)
        .replace("Y", sprite.offset_y);
    })
    .join("\n");

  return shared + "\n" + perSprite;
};
```

### 在vue.config.js中增加如下代码：

```
module.exports = {
  configureWebpack: config => {

    /*
    Readme里面有这句话resolve contains location of where generated image is
    （要把生成的地址resolve到modules里面。不写就报错）
    */
    config.resolve.modules = ["node_modules", "assets/sprite"];
    // 定义一个插件数组。用来覆盖，在里面使用我们的主角
    const Plugins = [
      new SpritesmithPlugin({
        /*
        目标小图标，这里就是你需要整合的小图片的老巢。
        现在是一个个的散兵，把他们位置找到，合成一个
        */
        src: {
          cwd: path.resolve(__dirname, "./src/assets/spriteDetail"), // 要创建雪碧图的源文件夹
          glob: "*.png"
        },
        // 输出雪碧图文件及样式文件，这个是打包后，自动生成的雪碧图和样式，自己配置想生成去哪里就去哪里
        target: {
          image: path.resolve(__dirname, "./src/assets/_sprite.png"), // 生成雪碧图目标路径与名称
          // 设置生成CSS背景及其定位的文件或方式
          css: [
            [
              path.resolve(__dirname, "./src/scss/_sprite.scss"),
              {
                // ./src/assets/scss/spr.scss
                format: "function_based_template"
              }
            ]
          ]
        },
        // 自定义模板入口，我们需要基本的修改webapck生成的样式，上面的大函数就是我们修改的模板
        customTemplates: {
          function_based_template: templateFunction
        },
        // 样式文件中调用雪碧图地址写法（Readme这么写的）
        apiOptions: {
          cssImageRef: "~@/assets/_sprite.png" // css文件中引用雪碧图的相对位置路径配置
        },
        // 让合成的每个图片有一定的距离，否则就会紧挨着，不好使用
        spritesmithOptions: {
          padding: 10
        }
      })
    ];
    // config里面，覆盖掉以前的，要不然不好使
    config.plugins = [...config.plugins, ...Plugins];
  },

};

```

## 3  生成精灵图 _sprite.png和 _sprite.scss文件

在项目根目录执行

```
npm run serve
```

跑完代码后会生成_sprite.png和 _sprite.scss文件，如图所示：

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/sprite/createFile.png)

## 4  引入样式

### （1）在根目录的main.js或者main.ts文件中添加代码：

```
import "./scss/_sprite.scss";
```

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/sprite/importScss.jpg)

###  (2)在Helloword.vue中使用样式

使用规则：添加一个<i>标签，class类固定为”icon icon-图片名称“

```
<i class="icon icon-training"></i>

```

###  浏览器显示

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/sprite/browser.jpg)








