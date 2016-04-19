# 拍照API `chanjet-plgin-take-photo`

提供拍照功能 , 目前支持chanjet平台, 后期增加微信.



## 安装

```
npm install chanjet-plugin-take-photo
```





## API



1. #### takePhoto

##### 参数

- options `Object` 设置选项
  - quality `number` 图片质量 , 0 : 高(默认) , 1 : 中 , 2 : 低
- callback `function` 执行完成后回调
- requestId `string` 应用自己定义的id , 用于在restore时判断使用





## 用法

```javascript
import TakePhotoPlugin from 'chanjet-plugin-take-photo'

let plugin = new TakePhotoPlugin();

//定义调用参数
const options = {
  quality : 0
};


//定义requestId 
//requestId用于在restore时帮助应用判断调用插件的业务或者逻辑.从而根据结果进行后续操作
const requestId = 'takePhotoAtDemoPage';



//定义回调
const callback = (rs) => {
  /*
   *  rs = {
   *		resultCode : number,	//0:ok , 1:failed , 2:canceled
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

}



/**
 * 参数说明
 * @param options
 *      @property options.quality 0:高质量(默认) , 1:中等质量 , 2:低质量
 * @param callback 执行完成后回调
 * @param requestId 应用自己分配的值,用于在restore时判断数据来源进行后续操作.
 *
 */
plugin.takePhoto(options , callback , requestId);
```