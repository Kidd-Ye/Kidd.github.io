# vue-cli3 配置全局样式

## 1  创建SCSS文件夹

在src目录下创建scss文件夹用于存放样式文件。如下图的文件结构所示：

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/globalScss/docStru.png)

## 2  创建 _variables.scss和 _index.scss

创建_variables.scss文件用于定义全局样式变量，比如我设置文字的颜色样式为红色。

```
$textColor:red;
```

创建_index.scss作为一个统一入口，用于引入开发者编写的各种样式文件。此例我先引入上个步骤编写的全局变量。

```
@import "variables";
```

## 3  创建vue.config.js

使用vuecli3创建的demo中是没有自带vue.config.js这个配置文件的，所以我们可以自己创建，在项目的根目录中创建并写入以下代码：

```
module.exports = {
  css: {
    // css预设器配置项
    loaderOptions: {
      sass: {
        prependData: `@import "~@/scss/index.scss";`
      }
    },
  }
};
```

该配置的简要意思就是通过css预设器加载指定的样式文件，作为全局样式。

## 4  在vue文件中使用样式

我们可以通过vuecli3.0中已经预先创建的Helloword.vue文件设置样式

```
.myColor{
  color:$textColor;
}
```

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/globalScss/textColor.png)

## 5  查看效果

在命令行输入 npm run serve

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/globalScss/result)

所以，通过这5 步操作即可轻松引入全局样式。希望帮到您。




