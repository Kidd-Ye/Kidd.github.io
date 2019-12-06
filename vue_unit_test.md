# 用Jest测试单文件组件

在项目中使用单元测试，本文使用的技术栈为：Jest + Vue Test Utils + sinon

* Jest 是一个由 Facebook 开发的测试运行器。
* Vue Test Utils 是 Vue.js 官方的单元测试实用工具库。
* sinon是个测试辅助工具,主要使用spy, stub, mock这三个方法。

## 1  准备工作

#### （1）若项目未曾使用过单元测试，按照官方文档一步一步操作。具体链接如下：

[用 Jest 测试单文件组件](https://vue-test-utils.vuejs.org/zh/guides/testing-single-file-components-with-jest.html)

#### （2）根目录下创建jest.config.js

将之前写进package.json中的有关jest的配置移动到这个文件中。

```
module.exports = {
    moduleFileExtensions: [
        "js",
        "json",
        "vue"
    ],
    transform: {
        ".*\\.(vue)$": "vue-jest",
        "^.+\\.js$": "<rootDir>/node_modules/babel-jest"
    },
    moduleNameMapper: {
        "^@/(.*)$": "<rootDir>/static_dev/$1"
    }
}
```

####（3）添加全局变量模拟axios请求

在jest.config.js中添加如下代码

```
module.exports = {
    ...
    // 增加    
    globals: {
        $axios: axiosss
    }
}

// 模拟axios请求，当url为“/url/path”时，返回自定义数据
let axiosss = function (url, data, scb, fcb) {
    let urlData = {
    	"/url/path": [[data: something]]
    }
    scb(urlData[url]);
}

```

## 2  编写测试代码

##### （1）在根目录下创建文件夹“unit_ test”, 在unit_ test文件夹下创建一个exapmle.spec.js

```
import { mount } from '@vue/test-utils'
import Component from 'component/path"

describe('Component', () => {

	test('is a Vue instance', () => {
		let wrapper = mount(Component);
    	expect(wrapper.isVueInstance()).toBeTruthy()
	});
});

```
执行npm run test

##### （2）拿ODN项目的一个页面进行实战，比如：客户业务单列表

修改exapmle.spec.js

```
import { mount } from '@vue/test-utils'
import Component from '../static_dev/miot_app/script/plugin2x/businessOrder/orderListPlugin.vue"

describe('Component', () => {

	test('is a Vue instance', () => {
		let wrapper = mount(Component);
    	expect(wrapper.isVueInstance()).toBeTruthy()
	});
});
```

然后执行npm run test，报出各种错误，下面逐一解决。

###### A.饿了么UI的组件报错

```
[Vue warn]: Unknown custom element: <el-input> - did you register the component correctly? For recursive components, make sure to provide the "name" option.
```

解决方法如下：

```
// exapmle.spec.js中添加以下代码
import Vue from "vue"
import ElementUi from "element-ui"

Vue.use(ElementUi);
```

###### B.$route中的属性值找不到

```
报错提示：let status = this.$route.query.status;

TypeError: Cannot read property 'query' of undefined

```
解决方法如下：

```
import { mount } from '@vue/test-utils'
import Component from '../static_dev/miot_app/script/plugin2x/businessOrder/orderListPlugin.vue'
import Vue from "vue"
import ElementUi from "element-ui" // 解决饿了么组件引入报错

Vue.use(ElementUi);// 解决饿了么组件引入报错

// 解决$route中的属性值找不到
const $route = {
    query: {
        status: 0
    }
};

describe('Component', () => {
    let wrapper = mount(Component, {
        mocks: {
            $route // 解决$route中的属性值找不到
        }
    });
    let vm = wrapper.vm;
    test('is a Vue instance', () => {
        expect(wrapper.isVueInstance()).toBeTruthy()

    });
});

```

###### C.方法找不到

```
TypeError: (intermediate value).format is not a function

  267 |       if (timeRange) {
  268 |         if (this.startTime !== timeRange[0]) {
> 269 |           this.startTime = new Date(timeRange[0]).format("YYYY-MM-DD hh:mm:ss");
      | ^
  270 |         }
  271 |         if (this.endTime !== timeRange[1]) {
  272 |           this.endTime = new Date(timeRange[1]).format("YYYY-MM-DD") + " 23:59:59";

```

解决如下：

```
可以通过在挂载选项中传入 methods 来覆写 config 中的方法集合。

import { mount, config } from '@vue/test-utils'
// 这个配置只能加在describe方法之外，否则不能生效。
config.methods['getStartEndTime'] = () => {
    //
};
```
使用断言判断axios请求后的数据变化。


以上三个问题解决后，执行npm run test，测试程序顺利执行通过。

## 3  sinon的使用

在项目中，一个模块的方法内常常会去调用另外一个模块的方法。在单元测试中，我们可能并不需要关心内部调用的方法的执行过程和结果，只想知道它是否被正确调用即可，甚至会指定该函数的返回值。此时，使用Mock函数是十分有必要。

Mock函数提供的以下三种特性，在我们写测试代码时十分有用：

* 捕获函数调用情况
* 设置函数返回值
* 改变函数的内部实现

jest也提供了相应的方法实现mock函数，详情参考：[jest.fn() spyOn() mock()](https://www.jianshu.com/p/ad87eaf54622)

### jest.fn()

将客户业务单页面中使用的一个method进行监听

```
test('测试jest.fn()调用', () => {
        let mockFn = jest.fn();
        wrapper.setMethods({
            searchDatas: mockFn,
        })
        vm.searchDatas();
        vm.searchDatas();
        expect(mockFn).toHaveBeenCalled();
        // 断言mockFn被调用了一次
        expect(mockFn).toBeCalledTimes(2);
    });
    
```

本文主要介绍sinon的三个实用方法：spy、stub、mock。首先，安装sinon。

```
npm install sinon -D
```

### （1）spy 间谍
##### spy即间谍，个人认为就是一个监听函数，以下是监听客户业务单页面中使用到的一个method，并判断其调用次数。

```
it("sinon.spy", ()=>{
        // vm = wrapper.vm;
        let spy = sinon.spy(vm, "searchDatas"); 

        vm.searchDatas();
        vm.searchDatas();

        expect(spy.called).toBeTruthy();
        expect(spy.callCount).toBe(2);
    })
    
```

### （2）stub 存根

##### stub即存根，就是监听到指定的函数并且可以替换掉函数的实现。

```
it("sinon.stub", ()=>{
        let stub = sinon.stub(vm, "searchDatas");
        stub.callsFake(()=>{
            console.log("使用stub 函数 searchDatas");
        });

        vm.searchDatas();
        vm.searchDatas();

        expect(stub.called).toBeTruthy();
        expect(stub.callCount).toBe(2);

        stub.restore();
    });

```

### （3）mock 模拟

##### mock像spy和stub一样的伪装方法, 不过mock没有得到期望的结果就会测试失败。主要步骤如下：

* 首先对某个函数的操作次数做预判
* 执行某个函数
* 验证预判是否符合

```
it("sinon.mock", ()=>{
        let mock = sinon.mock(vm);

        mock.expects("searchDatas").once();// 预期
        mock.expects("getStartEndTime").twice();

        vm.searchDatas();// 对函数实际操作
        vm.getStartEndTime();// 对函数实际操作
        vm.getStartEndTime();// 对函数实际操作

        mock.verify();// 验证预期
    });

```


## 4  Istanbul  测试覆盖率

伊斯坦布尔测试覆盖率从以下四个维度统计：

* Statements: 语句覆盖率，所有语句的执行率；
* Branches: 分支覆盖率，所有代码分支如 if、三目运算的执行率；
* Functions: 函数覆盖率，所有函数的被调用率；
* Lines: 行覆盖率，所有有效代码行的执行率，和语句类似，但是计算方式略有差别；

具体可以参考以下文章：[Istanbul](https://segmentfault.com/a/1190000019817317)
[测试覆盖率的认识](https://www.cnblogs.com/nianmumu/p/8417472.html)
