# Vue-cli 3.0 项目run build后打开index.html一片空白

使用vuecli3.x创建的项目，npm run build之后，在生成的dist目录下打开index.html，浏览器显示一片空白。以下是解决方法。

## 1.vue.config.js配置publicPath
 
```publicPath: './'``` 

百度了很多文章，都是说配置了这个就可以了。然并卵。还需要查看一下路由配置。


## 2.在项目路由配置文件中修改mode

```
const router = new VueRouter({
  mode: process.env.NODE_ENV === "production" ? "hash" : "history",
  base: process.env.BASE_URL,
  routes
});
```

其中最关键的是这句：
```
mode: process.env.NODE_ENV === "production" ? "hash" : "history",
```

### 具体详情如下：

配置路由模式:

hash: 使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器。

history: 依赖 HTML5 History API 和服务器配置。

abstract: 支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式。

### 结论
如果使用history模式上线，必须要服务端在服务器上有对应的模式才能使用history（看上面链接），如果服务器上没有配置，可以先使用默认的hash；

参考文章：https://blog.csdn.net/zhengbusi/article/details/98184628