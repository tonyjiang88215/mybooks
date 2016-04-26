# 电话API  `chanjet-plugin-phone-call`

提供电话的api , 目前支持chanjet平台, 后期增加微信支持.



### 安装

```
npm install chanjet-plugin-phone-call
```



## API

1. #### call 读取短信

   ##### 参数

   - phoneNo `string` 电话号码
   - callback `function` 执行完成后回调



## 用法

```javascript
//加载插件
import SMSPlugin from 'chanjet-plugin-phone-call'

//初始化  
let plugin = new PhoneCallPlugin();


/************** 打电话 **************/

const phoneNo = '13810343454';

const phoneCallCallback = (rs) => {
  //通过rs.result判断是否操作成功
  if(rs.resultCode == 0){
    //成功
  }else{
    //失败
  }
}

//调用读取短信api
plugin.call(phoneNo , phoneCallCallback);

```

