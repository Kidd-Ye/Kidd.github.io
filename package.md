# Electron打包桌面程序
>墙裂推荐文章：
>[参考链接](https://www.jianshu.com/p/59e4fe80e9d9)


## 下载demo

>先从git中下载：[electron-quick-start](https://github.com/electron/electron-quick-start)

>下载后解压缩可见目录结构如下：

>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p6.png)

## 安装打包插件

>打开命令行，在项目的根目录执行以下命令：

```
npm install

```


>此时项目目录多了一个node_modules文件夹，继续执行命令安装打包插件electron-packager：


```
npm i electron-packager --save-dev

```

## 新建app和dist文件夹

>新建app和dist文件夹，app文件夹中包含静态文件，dist文件夹用来存放打包后的执行文件。
>>cd 进入app目录，将index.html、package.json、package-lock.json、renderer.js都拉进app文件夹中，在app目录下执行：
>>
>>```
>>npm install

>>```
>>切勿使用cnpm install,通过cnpm装的node_module，由于所有的包都是扁平化的安装，一下子node_modules展开后有非常多的文件。导致了在electron-packager打包的过程中非常慢。但是如果改用npm来安装node_modules的话，所有的包都是树状结构的，层级变深。 但是打包速度会快很多。
>>
>>现在的目录结构如下：
>>
>>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p7.png)
>>

## 配置package.json
>在根目录的package.json中增加两句代码
>
>```
>"packageDarWin": "electron-packager ./app myapp --platform=darwin --arch=x64 --icon=favicon.icns --out=./dist --asar --app-version=1.0.0 --overwrite --electron-version=4.0.1",
"packageWin": "electron-packager ./app myapp --platform=win32 --arch=x64 --icon=favicon.ico --out=./dist --asar --app-version=1.0.0 --overwrite --electron-version=4.0.1"
>```
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p8.png)
>
>
>打包不同平台下的配置不完全相同，可以在网上搜搜有很多讲解这些信息是干嘛的，注意在打包时icon图标信息最好有，否则有可能会打包失败。
>
>


## 添加程序图标
>
>打包成win的执行程序时，需要.icon后缀的图片
>
>打包Mac的执行程序时，需要.icns后缀的图片
>
>可以在网上搜索在线转换，方便快捷。图片准备好后直接放到根目录下
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p9.png)
>


## 打包
>在electron-quick-start目录下，也就是项目的根目录下执行以下命令：
>
>```
>npm run packageWin
>npm run packageDar
>
>```
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p10.png)
>
>打包成功如图所示，在dist文件夹下会多出两个文件夹
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p11.png)
>
>
>最后，进入文件夹双击图标即可启动程序了。
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p12.png)
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p13.png)
>
>![img](https://github.com/Kidd-Ye/Kidd.github.io/blob/master/img/p14.png)
>
>
>

## Demo
>项目已经上传至[git](),可以下载参考学习。
>





