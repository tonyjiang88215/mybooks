# 拍照API `chanjet-plgin-take-photo`

提供拍照功能 , 目前支持chanjet平台, 后期增加微信.



### 安装

```
npm install chanjet-plugin-take-photo
```



### 用法

```javascript
import TakePhotoPlugin from 'chanjet-plugin-take-photo'

let plugin = new TakePhotoPlugin();

plugin.takePhoto((rs) => {
  /*
   *  rs = {
   *		result : number,	//0:ok , 1:failed , 2:canceled
   *		message : string,	
   *		requestId : string,
   *		body : {
   *			data : Object
   *		}
   *  }
   */
  
  
  //调用成功
  if(rs.result == 0){
	//插入应用自己的代码
    console.log(rs.body);
    
  //调用失败
  }else if(rs.result == 1){
  	//插入应用自己的代码
    console.log(rs.message);
    
  //用户取消
  }else{
  	//插入应用自己的代码
  }
  
});

```

