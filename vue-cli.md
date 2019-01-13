# Vue项目简易搭建
搭建vue框架前，先安装四样东西


## 1.安装Node.js


## 2.设置淘宝镜像
设置国内镜像：[参考链接](https://npm.taobao.org/)

```
npm config set registry https://registry.npm.taobao.org 
```

## 3.vue-cli脚手架的安装
建议全局安装 

```
npm install -g vue-cli
```


## 4.安装webpack 
建议全局安装 

```
npm install -g webpack
```

四样准备就绪后，开始创建项目

## 建立项目
vue_project 可以自己指定名称

```
vue init webpack vue_project
```

可见到如图所示的目录结构（node_modules文件夹除外）

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p2.png)

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p3.png)


## 运行项目

```
cd vue_project
npm run dev
```

当项目跑起来后，用浏览器输入

```
http://localhost:8080
```

若看到以下界面，说明项目正常运行起来了。

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p4.png)





