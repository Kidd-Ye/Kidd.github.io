# An Async Example For UnitTest
单元测试之异步示例


## 1  引入axios

```
//example.spec.js

import http from "axios";
```


## 2  写一个网络请求

使用天气预报网站的get接口用作测试接口，可直接调用。

```
//example.spec.js

function getList() {
	return new Promise((resolve, reject) => {
		http.get("http://wthrcdn.etouch.cn/weather_mini?citykey=101070101").then(res => {
			resolve(res);
		}).catch(reject);
	});
}

```

## 3  测试代码

使用天气预报网站的get接口用作测试接口，可直接调用。请求返回的status为200即访问成功。

```
//example.spec.js

describe('接口测试', () => {

	it('获取json', () => {
		return getList().then(res => {
			if(res.status == 200){
				console.log("data",res.data)
			}
			expect(res.status).toBe(200);
		}).catch((err) => {
			expect(err.response.status).toBe(502);
		});
	});
});

```

## 4  启动测试

命令行输入,或者根据package.json定义的执行脚本启动测试。

```
npm run test

```

#### 测试结果

```
 PASS  unit_test/exapmle.spec.js
  接口测试
    ✓ 获取json (139ms)

  console.log unit_test/exapmle.spec.js:47
    data { data:
       { yesterday:
          { date: '19日星期四',
            high: '高温 -5℃',
            fx: '北风',
            low: '低温 -16℃',
            fl: '<![CDATA[3-4级]]>',
            type: '多云' },
         city: '沈阳',
         forecast: [ [Object], [Object], [Object], [Object], [Object] ],
         ganmao: '昼夜温差很大，易发生感冒，请注意适当增减衣服，加强自我防护避免感冒。',
         wendu: '-4' },
      status: 1000,
      desc: 'OK' }

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        2.28s
Ran all test suites.


```








