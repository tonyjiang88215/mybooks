# 认证API `chanjet-plugin-auth`

在mutants框架中, 提供认证,信息查询相关api , 目前支持chanjet平台.

**不能脱离mutants框架单独使用.**



## 获取实例

```javascript
//通过mutants来获取插件实例
const plugin = mutants.plugin.auth;
```



## API

1. #### getConfig 获取企业信息

   ##### 返回值

   ```javascript
   var result = {
   "resultCode": 0,
   "message": "",
   "requestId": null,
   "body": {
     "data": {
       "Host": "gzq.chanjet.com",
       "version": "3.1.1.001",
   	"auth": "",
       "userid": "60003784742",
       "deviceInfo": {
         	"availableMemory": "16027648",
   		"deviceId": "99000558811994",
         	"deviceType": "APH",
         	"manufacturer": "YuLong",
         	"model": "Coolpad 8297-C00",
         	"networkStatus": "WIFI",
         	"osRelease": "4.4.4",
         	"usedMemory": "268435456"
       },
       "domain": "https://58.83.201.95",
       "entAvatar": "http://sto.chanapp.chanjet.com/4a47ecad-3fcd-422b-879b-b2df91606e00/2015/03/25/1427273343666.png.crop.png.comp.png",
       "entId": "90004304382",
       "entName": "我的企业好1呵呵",
       "ext": null,
       "page": "home",
       "params": {"id": null},
       "platformExtension": "",
       "tab": "0",
       "userAvatar": "https://sto.chanapp.chanjet.com/a31cad70-142e-44f3-85ab-488629ec0275/cia/headpictrue/2014/09/15/18604b7a84e5468fb858595ddf9ce585.jpg",
       "userName": "开放平台-郑江",
       "back_to_native": true,
       "appId": 3
           }
       }
   }
   ```

   ​

2. #### getAuthCode 获取认证code

   ##### 返回值

   ```javascript
   var result = {
     resultCode : 0,
     message : "",
     body : {
       data : {
         auth_code : "0806f0e153c547eb95c89bfb3ff03ecd"
       }
     }     
   }
   ```







## 用法

```javascript
//加载插件
const plugin = mutants.plugin.auth;


/********** 获取企业信息 **********/
plugin.getConfig( (rs) => {

  if(rs.resultCode == 0){//成功
    console.log(rs.body.data);
  }else{//失败
  }

});


/********** 获取authCode **********/
plugin.getAuthCode( (rs) => {

  if(rs.resultCode == 0){//成功
    console.log(rs.body.data);
  }else{//失败
  }

});

```



## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `chanjet-plugin` 提供的 `PluginMocker`来设置mock数据.



### 模拟成功

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  AuthPlugin : {
    //获取企业信息
    getConfig: {
            status: 'success',
            data: {
                "Host": "gzq.chanjet.com",
                "version": "3.1.2.001",
                "auth": "",
                "userid": "60003784742",
                "deviceInfo": {
                    "availableMemory": "15962112",
                    "deviceId": "99000558811994",
                    "deviceType": "APH",
                    "manufacturer": "YuLong",
                    "model": "Coolpad 8297-C00",
                    "networkStatus": "WIFI",
                    "osRelease": "4.4.4",
                    "usedMemory": "268435456"
                },
                "domain": "https://58.83.201.95",
                "entAvatar": "http://www.example.com/enterprice/pic.png",
                "entId": "90004304382",
                "entName": "enterprice_name",
                "ext": null,
                "page": "home",
                "params": {"id": null},
                "platformExtension": {
                  	"ciaAppId": 7,// cia应用ID
                  	"startTimestamp": 1457280000000,// 超始时间戳 unix时间戳
                  	"subscribeType": 1,// 应用开通方式，1：付费开通，2：试用开通；
                  	"endTimestamp": 1488816000000,// 结束时间戳 unix时间戳
                  	"domain": "http://ul0r6mvjo1hr.chanapp.com/",// 虚机域名
                  	"orgAccount": "ul0r6mvjo1hr"// 虚机账号
    			},
                "tab": "0",
                "userAvatar": "https://www.example.com/user/head/pic.png",
                "userName": "user_name",
                "back_to_native": true,
                "appId": 3
            }
        },
    
    //获取authCode
    getAuthCode: {
      status: 'success',
      data: {
        //在mock时 , auth_code请通过正常途径获取
        auth_code : 'e2f832270f4f47e29ea63383c6bc383c'
      }
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
  AuthPlugin : {
    getConfig : {
      status : 'failed',
      message : '网络异常,请稍后再试'
    },
    getAuthCode : {
      status : 'failed',
      message : '网络异常,请稍后再试'
    }
  }

}

//设置mock数据
mutants.plugin.setMockData(mockData);
```





