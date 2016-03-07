##### Ajax-Interceptor `V0.1.0`

不要被ajax的名字所蛊惑 , 其实这并不是一个Ajax库, 而是针对应用请求401状态的一种处理 . 本类库有以下功能:

- 当访问指定域名的请求返回401时 , 我们会将它放入重发队列;
- 重新从cia查询用户登陆状态, 并调用指定接口进行codeLogin;
- codeLogin成功后, 依次发送重发队列中的请求;
- codeLogin失败后, 依次触发重发队列中的Error回调;

## 使用

#### 安装

``` 
npm install @cjt/ajax-interceptor
```

使用npm安装.



#### 启动

在应用初始化时 , 添加以下代码 , 就可以保证在请求返回401时,自动进行重新登陆并且重发请求了.

``` javascript
import {ZeptoAjaxInterceptor} from '@cjt/ajax-interceptor'


let ajaxInterceptor = new ZeptoAjaxInterceptor($.ajax , {
  	//应用在虚拟机上的根目录,必填
	appRootUrl : "http://u4ihsgo5u78e.chanapp.com/chanjet/accounting",
	//应用的client_id,不知道的找后端同学或者CIA,必填
  	client_id : "accounting",
  	//http协议类型,选填,默认值为http:  可选值:['http:','https:']
  	protocol : "http:" 
});
ajaxInterceptor.init();
```



#### 实现思路

具体实现401重发机制的大致思路如下:

​	1.在ajax发送之前,记录指定域名的请求的时间戳;

​	2.重写请求的错误回调,判断http-code是否为401:

​		如果是,则添加到重发队列,等待处理;

​		如果不是,则直接调用应用的错误回调;

​	3.添加到重发队列之前,先检查请求时间和上次codeLogin的时间,以保证尽量少的调用codeLogin;

​	4.ajaxInterceptor进行codeLogin:

​		如果成功,将队列中的请求依次重发;

​		如果失败,将队列中的请求依次调用应用的错误回调;



​	如果对具体实现有兴趣, 可以参考源码.

