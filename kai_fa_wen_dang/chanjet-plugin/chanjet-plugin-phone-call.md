# 电话API  `chanjet-plugin-phone-call`

在mutants框架中, 提供电话的api , 目前支持chanjet平台, 后期增加微信支持.

**不能脱离mutants框架单独使用.**



## 获取实例

```javascript
//通过mutants来获取插件实例
const plugin = mutants.plugin.phone;
```





## API

1. #### call 打电话

   ##### 参数

   - phoneNo `string` 电话号码
   - callback `function` 执行完成后回调



## 用法

```javascript
//获取插件实例
const plugin = mutants.plugin.phone;




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



## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `mutants.plugin.setMockData` 来设置mock数据.

具体参考如下:



### 模拟成功

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  PhoneCallPlugin: {
    //打电话
    call: {
      status: 'success'
    }
  }
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```



### 模拟失败

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  PhoneCallPlugin: {
    //打电话
    call: {
      status: 'failed',
      message : '没有权限'
    }
  }
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```





