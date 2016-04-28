# 预览API `chanjet-plugin-peview`

提供预览功能 , 目前提供图片预览, 后续可能支持其他文件预览.

目前支持chanjet平台 , 后期增加微信.



## 安装

```
npm install chanjet-plugin-preview
```



## API



1. #### previewImg

   ##### 参数

   - options `Object` 设置选项
     - imgList `Array` 需要预览的图片集合
     - firstIndex `number` 首先展示第几张图片, 默认值:0
     - canDelete `Boolean` 是否可以在预览时删除图片, 默认值:false
   - callback `function` 执行完成后回调
   - [requestId] `string` 应用自己定义的id , 用于在restore时判断使用 , 选填

   ##### 返回值

   - result
     - resultCode 操作结果 0:成功 , 1:失败
     - message 消息
     - body
       - data 如果在预览时删除图片 , 这里会返回被删除的图片数据





## 用法

```javascript
import PreviewPlugin from 'chanjet-plugin-preview'

let plugin = new PreviewPlugin();

//定义调用参数
const options = {
    imgList : [
      'http://img4.imgtn.bdimg.com/it/u=2134987970,41197490&fm=21&gp=0.jpg' ,
      'http://bbs.zgwg.com.cn/UploadFile/2009-4/200941820512789561.jpg'
    ],
    firstIndex : 0,
  	canDelete : 1
  
};


//定义requestId 
//requestId用于在restore时帮助应用判断调用插件的业务或者逻辑.从而根据结果进行后续操作
//预览操作不进行转场,所以在目前情况下不会被销毁,可以选择不传requestId
const requestId = 'PreviewAtDemoPage';


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
  if(rs.resultCode == 0){
	//插入应用自己的代码
    console.log(rs.body);

  //调用失败
  }else if(rs.resultCode == 1){
  	//插入应用自己的代码
    console.log(rs.message);

  //用户取消
  }else{
  	//插入应用自己的代码
  }
}




/**
 * 预览图片
 * @param options {JSONObject} 设置
 *  @property options.imgList {Array}  预览图片的集合
 *  @property options.firstIndex  {Number} 首先展示第几张图片, 默认值:0
 * @param callback 执行完成后回调
 * @param [requestId] 应用自己分配的值,用于在restore时判断数据来源进行后续操作.
 */
plugin.previewImg(options , callback , requestId);
```





## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `chanjet-plugin` 提供的 `PluginMocker`来设置mock数据.



### 模拟成功

```javascript
import {PluginMocker} from 'chanjet-plugin-base';

const mockData = {
  //mock数据中,键名为插件的类名
  PreviewPlugin : {
    status : 'success',
  }
}

//设置mock数据
PluginMocker.data = mockData;
  
  
  
```



### 模拟失败

```javascript
import {PluginMocker} from 'chanjet-plugin-base';

const mockData = {
  //mock数据中,键名为插件的类名
  PreviewPlugin : {
    status : 'failed',
  }
}

//设置mock数据
PluginMocker.data = mockData;
```







