# Vue-cli 3.0 项目简易搭建

以下的安装都是在 macOS 的环境下进行的，当然在 windows 和 linus 下也同理。

## 1.vue-cli脚手架的安装
vue cli 的包名称由 vue-cli 改成了 @vue/cli。 如果你已经全局安装了旧版本的 vue-cli (1.x 或 2.x)，你需要先通过 
```npm uninstall vue-cli -g``` 
或 
```yarn global remove vue-cli ```卸载它。使用下列任一命令安装这个新 vue-cli 3.0.3 的包：

```
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```


## 2.创建项目

* 新建文件夹，在该文件夹下打开命令窗口，输入以下命令进行新建项目，当然我起的项目名字叫 vue-webpack-demo

```
vue create vue-webpack-demo
```

* 会让你选择默认（default）还是手动（Manually）

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/vuecli3/1.jpg)

* 选择手动配置，配置列表中列举的内容如下

```
1.Babel //是否使用babel编译代码
2.TypeScript //是否使用TypeScript
3.Progressive Web App (PWA) Support //支持渐进式网页应用程序
4.Router //路由管理器
5.Vuex //状态管理模式（构建一个中大型单页应用时）
6.CSS Pre-processors //css预处理
7.Linter / Formatter //代码风格、格式校验
8.Unit Testing // 单元测试
9.E2E Testing // 即端对端测试
空格选中，上下键切换，回车确认，具体配置见下图
```


![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/vuecli3/config.jpg)


```
1、 TypeScript
是否使用class风格的组件语法，是
Use class-style component syntax?

是否使用babel做转义，是
Use Babel alongside TypeScript for auto-detected polyfills?

2、Router
路由使用历史模式，一般实际项目要使用history
Use history mode for router? (Requires proper server setup for index fallback in production) 

3、CSS Pre-processors css预处理，我用的node-sass
Pick a CSS pre-processor (PostCSS， Autoprefixer and CSS Modules are supported by default)  
  Sass/SCSS (with dart-sass)
  Sass/SCSS (with node-sass)
  Less
  Stylus

4、Linter / Formatter 代码风格、格式校验，选择ESLint + Prettier
  TSLint
  仅错误预防
  ESLint with error prevention only
  Airbnb配置
  ESLint + Airbnb config
  标准配置
  ESLint + Standard config
  Prettier配置（常用）
  ESLint + Prettier

5、选择lint方式：Pick additional lint features，选择保存时检查
保存时检查
Lint on save
提交时检查
Lint and fix on commit

6、Unit Testing 单元测试，使用Jest
Mocha + Chai
Jest

7、E2E Testing E2E（End To End）即端对端测试，不使用
Cypress (Chrome only) 
Nightwatch (Selenium-based)

8、选择 Babel，PostCSS， ESLint 等自定义配置的存放位置，在package.json里配置

In dedicated config files 在专用的配置文件中
In package.json 在package.json

9、将此作为将来项目的预置吗？是的，下次可以直接用
Save this as a preset for future projects?
10、项目配置名称，设置配置名称为：my-conf
Save preset as：my-conf

回车后开始安装

```


![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/vuecli3/config1.jpg)

## 运行项目

安装完毕后，执行以下命令：

```
cd vue-webpack-demo
npm run serve
```

### 浏览器打开

出现以下界面，说明运行成功。

![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/vuecli3/run.jpg)






