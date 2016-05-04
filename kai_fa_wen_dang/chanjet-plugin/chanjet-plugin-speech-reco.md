# 语音识别API `chanjet-plugin-speech-reco`

在mutants框架中,  提供语音转换文字功能.

**不能脱离mutants框架单独使用.**



## 获取实例

```javascript
//通过mutants来获取插件实例
const plugin = mutants.plugin.speechReco;
```





## API

1. ####start 开始识别
2. #### stop 停止识别

3. #### cancel 取消当前正在进行的识别操作





## 事件

1. #### onStart 开始事件

2. #### onSpeechStart 检测到开始说话事件

3. #### onSpeechEnd 检测到说话完成事件

4. #### onUpdateResult 动态更新识别内容

   返回值

   - result `Object` 返回对象

     - data `Array` 识别结果数组, 由识别结果组成, 识别结果是字符串类型.

5. #### onFinish 识别完毕事件

   返回值

   - result `Object` 返回对象
     - data `Array` 识别结果数组, 由识别结果组成, 识别结果是字符串类型.

6. #### onCancel 取消识别事件

7. #### onError 发生错误事件

   返回值

   - result `Object` 返回对象
     - errorCode `number` 错误码
     - message `string` 错误提示

   ​

   错误码对照表

| 错误码   | 对应错误类型          |
   | :---- | :-------------- |
   | 10001 | 客户端异常：位置错误      |
   | 10002 | 用户未说话           |
   | 10003 | 用户说话声音太短        |
   | 10004 | 语音前端库检测异常       |
   | 10005 | 处理超时            |
   | 20001 | 录音设备不可用         |
   | 20001 | 录音中断            |
   | 30001 | 网络不可用           |
   | 30002 | 网络发生错误          |
   | 30002 | 网络本次请求超时        |
   | 30004 | 解析失败            |
   | 40001 | 协议参数错误          |
   | 40002 | 识别过程出错          |
   | 40003 | 没有找到匹配结果        |
   | 40004 | AppnameUnkown错误 |
   | 40005 | 声音不符合识别要求       |
   | 40006 | 语音过长            |
   | 40007 | 未知错误            |
   | 50001 | 开始工作            |
   | 50002 | 没有麦克风权限         |
   | 50003 | 没有设定应用API KEY   |
   | 50004 | 获取accessToken失败 |
   | 50005 | 当前网络不可用         |
   | 50006 | 代理不可用           |
   | 50007 | 录音设备不可用         |
   | 50008 | 启动预处理模块出错       |
   | 50009 | 设置的识别属性无效       |


   


## 用法

```javascript
//获取插件实例
const plugin = mutants.plugin.speechReco;


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

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `mutants.plugin.setMockData` 来设置mock数据.

具体参考如下:



### 模拟成功

```javascript
/**
语音识别的mock比较特殊,由于存在过程,所以可以模拟用户说话的时间, 当用户点击停止时,还是会根据status进行返回结果.
**/

const mockData = {
  //mock数据中,键名为插件的类名
  SpeechRecoPlugin : {
    status : 'success',
	//模拟说话的时间,默认3000ms
    time : 1000,
    //模拟识别结果
    data : ['模拟语音识别结果','摸你余音识别机俄国','摸你依云识别结果']
  }

//设置mock数据
mutants.plugin.setMockData(mockData);
```



### 模拟失败

```javascript
import {PluginMocker} from 'chanjet-plugin-base';

const mockData = {
  //mock数据中,键名为插件的类名
  SpeechRecoPlugin : {
    status : 'failed',
    //模拟说话的时间,默认3000ms
    time : 1000,
    message : '语音识别失败'
  }
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```