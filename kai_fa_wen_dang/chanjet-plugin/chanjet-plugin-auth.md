# 认证API `chanjet-plugin-auth`

提供认证,信息查询相关api , 目前支持chanjet平台.



## 安装

```
npm install chanjet-plugin-auth
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
               "accessToken": "d58259e8-dedb-46b0-be20-8a29794fcfd6",
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

2. #### getAuthCode 

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
import AuthPlugin from 'chanjet-plugin-auth'

//初始化  
let plugin = new AuthPlugin();


/********** 获取企业信息 **********/
this.authPlugin.getConfig( (rs) => {
  
  if(rs.resultCode == 0){//成功
    console.log(rs.body.data);
  }else{//失败
  }
  
});


/********** 获取authCode **********/
this.authPlugin.getAuthCode( (rs) => {
  
  if(rs.resultCode == 0){//成功
    console.log(rs.body.data);
  }else{//失败
  }
  
});


```

