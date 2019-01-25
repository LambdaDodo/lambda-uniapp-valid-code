# Lambda-uniapp-valid-code
---
该模板是非常通用的手机验证码登陆页面，兼容APP、小程序、H5，不过没有测试支付宝小程序和百度小程序。


#### 文件说明
```
-pages/index/index.vue 引导页面
-pages/index/valid-code 验证码页面
-pages/index/number-key-board 键盘模板
```


#### 使用说明

```
pages/index/valid-code 页面中

使用uni.navigate(
	{url : 'pages/index/valid-code?mobile=1333282731'}
)
即可跳转到pages/index/valid-code 是验证码页面
```



