# 短信API  `chanjet-plugin-sms`

在mutants框架中,  提供读取短信的api , 只在chanjet平台上可用, 微信不提供此功能.

**不能脱离mutants框架单独使用.**



## 获取实例

```javascript
//通过mutants来获取插件实例
const plugin = mutants.plugin.sms;
```





## API

1. #### read 读取短信
   ##### 参数

   - options `Object` 设置选项
     - startDate `number` 读取开始时间戳
     - endDate `number` 读取结束时间戳
     - `选填` address `string` 要读取的手机号码
     - `选填` protocol `string` 读取短信协议
       - `sms` : 短信
       - `mms` : 彩信
     - `选填` read `string` 是否已读
       - `read` : 已读 
       - `unread` : 未读
     - `选填` type `string` 收到的短信还是发送的
       - `receive` : 收件箱
       - `send` : 发件箱
   - callback `function` 执行完成后回调


1. #### send 发送短信
   ##### 参数

   - options `Object` 设置选项
     - phoneNo `string` 读取开始时间戳
     - content `string` 读取结束时间戳
   - callback `function` 执行完成后回调

   ​




## 用法

``` javascript
//获取插件实例
const plugin = mutants.plugin.sms;



/************** 读取短信 **************/

const readSMSOptions = {
  //读取开始时间 , 必填
  startDate : new Date('2016','2').getTime(),	
  //读取结束时间 , 必填
  endDate : new Date().getTime(),
  //读取哪个手机号发过来的短信 , 选填 , 默认查所有手机号的
  address : '13810343454',
  //读取短信还是彩信(sms:短信, mms:彩信) , 选填 , 默认查所有
  protocol : 'sms',
  //读取已读短信还是未读短信(read:已读,unread:未读) , 选填 , 默认查所有
  read : 'read',
  //读取发出去的还是收到的短信(receive:收到的,send:发出去的) , 选填 , 默认查所有
  type : 'receive'
};

const readSMSCallback = (rs) => {
  //通过rs.result判断是否操作成功
  if(rs.resultCode == 0){
    //通过rs.data读取数据
  	console.log(rs.data);
  }else{

  }
}


//调用读取短信api
plugin.read(readSMSOptions , readSMSCallback);

/************** 发送短信 **************/

const sendSMSOptions = {
  //发送短信的手机号
  phoneNo : '13810343454',
  //发送短信的内容
  content : '测试发送短信内容'
};

const sendSMSCallback = (rs) => {
  console.log('sendSMS result : ' , rs );
}

//调用发送短信接口
plugin.send(sendSMSOptions , sendSMSCallback)
```



## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `mutants.plugin.setMockData` 来设置mock数据.

具体参考如下:





### 模拟成功

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  SMSPlugin: {
    //读取短信
    read : {
      status: "success",
      data: [
        {
          "_id": 3333, //短消息序号
          "thread_id": 0, //对话序号
          "address": "15926306304", //发件人地址
          "person": "henry", //发件人 返回一个数字就是联系人列表里的序号，陌生人为null
          "date": new Date().getTime(), //日期 long
          "protocol": 0, //协议 0 SMS_RPOTO, 1 MMS_PROTO
          "read": 1, //是否阅读 0未读， 1已读
          "status": 0, //状态 -1接收，0 complete, 64 pending, 128 failed
          "type": 1, //类型 1是接收到的，2是已发出
          "body": "", //消息内容
          "service_center": "" //短信服务中心号码编号
        },
        {
          "_id": 0, //短消息序号
          "thread_id": 0, //对话序号
          "address": "15926306304", //发件人地址
          "person": "henry", //发件人 返回一个数字就是联系人列表里的序号，陌生人为null
          "date": new Date().getTime(), //日期 long
          "protocol": 0, //协议 0 SMS_RPOTO, 1 MMS_PROTO
          "read": 1, //是否阅读 0未读， 1已读
          "status": 0, //状态 -1接收，0 complete, 64 pending, 128 failed
          "type": 1, //类型 1是接收到的，2是已发出
          "body": "", //消息内容
          "service_center": "" //短信服务中心号码编号
        },
        {
          "_id": 0, //短消息序号
          "thread_id": 0, //对话序号
          "address": "15926306304", //发件人地址
          "person": "henry", //发件人 返回一个数字就是联系人列表里的序号，陌生人为null
          "date": new Date().getTime(), //日期 long
          "protocol": 0, //协议 0 SMS_RPOTO, 1 MMS_PROTO
          "read": 1, //是否阅读 0未读， 1已读
          "status": 0, //状态 -1接收，0 complete, 64 pending, 128 failed
          "type": 1, //类型 1是接收到的，2是已发出
          "body": "", //消息内容
          "service_center": "" //短信服务中心号码编号
        }
      ]
    },

    
    //发送短信
    send : {
      status : 'success'
    }
    },
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```



### 模拟失败

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  SMSPlugin: {
    //读取短信
    read : {
      status: "failed",
      message : '读取失败'
    },

    
    //发送短信
    send : {
      status : 'failed',
      message : '没有权限'
    }
  }
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```



