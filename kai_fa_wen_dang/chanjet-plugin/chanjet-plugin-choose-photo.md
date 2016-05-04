# 读取相册API `chanjet-plgin-choose-photo`

在mutants框架中, 提供从相册中选择照片的功能 , 目前支持chanjet平台, 后期增加微信.

**不能脱离mutants框架单独使用.**



## 获取实例

```javascript
//通过mutants来获取插件实例
const plugin = mutants.plugin.choosePhoto;
```





## API



1. #### choosePhoto 选择照片

##### 参数

- options `Object` 设置选项
  - maxCount `number` 最大选图数量 , 默认值: 9
  - quality `number` 图片质量 , 0 : 高(默认) , 1 : 中 , 2 : 低
- callback `function` 执行完成后回调
- requestId `string` 应用自己定义的id , 用于在restore时判断使用





## 用法

```javascript
//获取插件实例
const plugin = mutants.plugin.choosePhoto;

//定义调用参数
const options = {
  maxCount : 9,
  quality : 0
};


//定义requestId 
//requestId用于在restore时帮助应用判断调用插件的业务或者逻辑.从而根据结果进行后续操作
const requestId = 'choosePhotoAtDemoPage';


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
 * 参数说明
 * @param options
 *      @property options.maxCount 最大选图数量, 默认9张
 *      @property options.quality 0:高质量(默认) , 1:中等质量 , 2:低质量
 * @param callback 执行完成后回调
 * @param requestId 应用自己分配的值,用于在restore时判断数据来源进行后续操作.
 *
 */
plugin.choosePhoto(options , callback , requestId);
```





## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `mutants.plugin.setMockData` 来设置mock数据.

具体参考如下:



### 模拟成功

```javascript
import {PluginMocker} from 'chanjet-plugin-base';

const mockData = {
  //mock数据中,键名为插件的类名
  ChoosePhotoPlugin : {
    status : 'success',
    //data为数组,其中包含了选择照片返回的照片地址,可自行mock
    data : ['http://www.example.com/1.png']
  }
}

//设置mock数据
PluginMocker.data = mockData;
  
  
  
```



### 模拟失败

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  ChoosePhotoPlugin : {
    status : 'failed',
    message : 'choose photo has been failed'
  }
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```



### 模拟取消

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  ChoosePhotoPlugin : {
    status : 'cancel'
  }
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```







