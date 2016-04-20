# 上传API `chanjet-plugin-upload`

提供图片和文件上传功能 , 目前支持chanjet平台 , 后期增加微信.



## 安装

```
npm install chanjet-plugin-upload
```



## API



1. #### uploadImg

   ##### 参数

   - imgList `Array` 上传图片的数组,数组项是本地图片路径.
   - callback `function` 执行完成后回调
   - requestId `string` 应用自己定义的id , 用于在restore时判断使用

   ​





## 用法

```javascript
import UploadPlugin from 'chanjet-plugin-upload'

let plugin = new UploadPlugin();

//定义调用参数
const uploadImgArray = [
  '/path/to/local/file1.png',
  '/path/to/local/file2.png',
  '/path/to/local/file3.png'
  ...
];


//定义requestId 
//requestId用于在restore时帮助应用判断调用插件的业务或者逻辑.从而根据结果进行后续操作
//上传操作不进行转场,所以在目前情况下不会被销毁,可以选择不传requestId
const requestId = 'uploadPhotoAtDemoPage';


//定义回调
const callback = (rs) => {
  /*
   *  rs = {
   *		resultCode : number,	//0:ok , 1:failed , 2:canceled
   *		message : string,	
   *		requestId : string,
   *		body : {
   *			data : Object , 	//具体数据格式参考下边的mock数据
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

    //上传失败后,通过rs.body.data.nativeUrl返回本次上传失败的文件
    //应用可以根据这个判断进行后续操作
	console.log(rs.body.data.nativeUrl);
    


  //用户取消
  }else{
  	//插入应用自己的代码
  }
}



/**
 * 参数说明
 * @param options
 *      @property options.maxCount 最大选图数量, 默认9张
 *      @property options.quality 0:高质量(默认) , 1:中等质量 , 2:低质量
 * @param callback 执行完成后回调
 * @param [requestId] 应用自己分配的值,用于在restore时判断数据来源进行后续操作.
 *
 */
plugin.choosePhoto(options , callback , requestId);
```





## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `chanjet-plugin` 提供的 `PluginMocker`来设置mock数据.



### 模拟成功

```javascript
import {PluginMocker} from 'chanjet-plugin-base';

const mockData = {
  //mock数据中,键名为插件的类名
  UploadPlugin : {
    status : 'success',
    //data为成功是返回的数据格式
    data : {
      nativeUrl : '/example/native/path/example.png',
      netUrl : {
        sizeInfo : {
          height : 200 ,
          width: 200,
          name : 'example_name',
          suffix : 'png',
          size : 10240,
          isOriginal : 0
        },
        uri : 'http://www.example.com/example.png'
      }
    }

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
  UploadPlugin : {
    status : 'failed',
    message : '上传失败',
    data : {
      nativeUrl : '/example/native/path/example.png',
      netUrl : {}
    }
  }
}

//设置mock数据
PluginMocker.data = mockData;
```

