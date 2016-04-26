# 语音识别API `chanjet-plugin-speech-reco`

提供语音转换文字功能.



## 安装

```
npm install chanjet-plugin-speech-reco
```



## API

1. ####start 开始识别
2. #### stop 停止识别

3. #### cancel 取消当前正在进行的识别操作

4. #### onStart 开始事件

5. #### onSpeechStart 检测到开始说话事件

6. #### onSpeechEnd 检测到说话完成事件

7. #### onUpdateResult 动态更新识别内容

   返回值

   - result `Object` 返回对象

     - data `Array` 识别结果数组, 由识别结果组成, 识别结果是字符串类型.

8. #### onFinish 识别完毕事件

   返回值

   - result `Object` 返回对象
     - data `Array` 识别结果数组, 由识别结果组成, 识别结果是字符串类型.

9. #### onCancel 取消识别事件

10. #### onError 发生错误事件


## 用法

```javascript
import SpeechRecoPlugin from 'chanjet-plugin-speech-reco'

let plugin = new SpeechRecoPlugin();

//识别开始
plugin.onStart( () => {
	console.log('启动识别');
});

//检测到说话开始
plugin.onSpeechStart( () => {
	console.log('开始说话');
});

//检测到说话结束
plugin.onSpeechEnd( () => {
	console.log('说话结束');
});

//动态返回识别结果
plugin.onUpdateResult( (rs) => {
  console.log('动态更新结果' , rs);
});

//识别完成
plugin.onFinish( (rs) => {
  console.log('处理完成' , rs);
});

//手动取消
plugin.onCancel( () => {
	console.log('手动取消');
});

plugin.onError( () => {
	console.log('出现错误');
});

//开始识别
plugin.start();

//停止识别
plugin.stop();

//取消识别
plugin.cancel();

```





## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `chanjet-plugin` 提供的 `PluginMocker`来设置mock数据.



### 模拟成功

```javascript
import {PluginMocker} from 'chanjet-plugin-base';

const mockData = {
  //mock数据中,键名为插件的类名
SpeechRecoPlugin : {
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
  SpeechRecoPlugin : {
    status : 'failed',
  }
}

//设置mock数据
PluginMocker.data = mockData;
```