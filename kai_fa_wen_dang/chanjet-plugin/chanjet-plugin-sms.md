# 读取短信API  `chanjet-plugin-sms`

提供读取短信的api , 只在chanjet平台上可用, 微信不提供此功能.



### 安装

``` 
npm install chanjet-plugin-sms
```



### 用法

``` javascript
//加载插件
import SMSPlugin from 'chanjet-plugin-sms'

//初始化  
let plugin = new SMSPlugin();

//调用读取短信api
plugin.read({
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
} , function(rs){
  //通过rs.result判断是否操作成功
  if(rs.result){
    //通过rs.data读取数据
  	console.log(rs.data);
  }else{

  }
})
```