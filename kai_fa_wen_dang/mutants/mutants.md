# Chanjet-Mutants `v0.0.5`

作为Mutants框架的入口,提供以下功能:

- 不同平台(工作圈 , 微信 , 钉钉等)的统一预处理.
- 环境检测
- native能力



## 加载

目前还是使用 `import` 方式进行进入 , 在适当时候 , 我们会将 `mutants` 更新到cdn服务器 , 使用`script`方式加载 . 目的是为了当工作圈native能力发生更新时 , `mutants` 提供的插件能力也能够同步更新 , 减少npm包管理导致的依赖复杂性.

我们会通过版本号来管理不同版本 , 这样可以兼容不同版本的工作圈.



## 安装

```shell
npm install chanjet-mutants
```



## ready

`mutants.ready` 作为 `mutants` 整个框架的入口 , 会先检测不同平台 native 能力是否准备完成 . 当准备完成后 , 将会执行通过 `ready` 传入的回调函数



```javascript
import mutants from 'chanjet-mutants';
  
mutants.ready( () => {
  //启动应用
});
  

```



## 环境检测

在 `mutants` 提供环境检测之前 , 环境检测是有 `chanjet-env-check` 这个包来完成的. 现在 `mutants` 中已经整合了环境检测 , 也是使用 `chanjet-env-check` , 挂载在 `mutants.env` 对象上. 

```javascript
import mutants from 'chanjet-mutants'

/*
mutants封装了chanjet-env-check对象,可以快速获取当前环境,无需在引入chanjet-env-check包,详见接口文档
*/

//当前平台
console.log(mutants.env.platform);
//当前系统或设备
console.log(mutants.env.os);
//当前浏览器
console.log(mutants.env.browser);

//可以通过constant来判断

//判断是否是chanjet平台
mutants.env.platform == mutants.constant.platform.chanjet
//判断是否是ios操作系统
mutants.env.os == mutants.constant.os.ios
//判断是否是chrome浏览器
mutants.env.browser == mutants.constant.browser.chrome
```



## Native能力

目前提供的Native能力 , 都可以在 `mutants.plugin` 对象上找到. 

具体能力见下表:

| API                              | Native能力               | 文档                                    |
| -------------------------------- | ---------------------- | ------------------------------------- |
| mutants.plugin.**auth**          | 企业信息及权限相关              | [去看看](../chanjet-plugin/chanjet-plugin-auth.md)         |
| mutants.plugin.**choosePhoto**   | 读取相册选照片                | [去看看](../chanjet-plugin/chanjet-plugin-choose-photo.md) |
| mutants.plugin.**takePhoto**     | 拍照                     | [去看看](../chanjet-plugin/chanjet-plugin-take-photo.md)   |
| mutants.plugin.**preview**       | 预览                     | [去看看](../chanjet-plugin/chanjet-plugin-preview.md)      |
| mutants.plugin.**upload**        | 上传                     | [去看看](../chanjet-plugin/chanjet-plugin-upload.md)       |
| mutants.plugin.**geo**           | 定位                     | [去看看](../chanjet-plugin/chanjet-plugin-geo.md)          |
| mutants.plugin.**phone**         | 电话                     | [去看看](../chanjet-plugin/chanjet-plugin-phone-call.md)   |
| mutants.plugin.**sms**           | 短信                     | [去看看](../chanjet-plugin/chanjet-plugin-sms.md)          |
| mutants.plugin.**share**         | 分享                     | [去看看](../chanjet-plugin/chanjet-plugin-share.md)        |
| mutants.plugin.**speechReco**    | 语音识别                   | [去看看](../chanjet-plugin/chanjet-plugin-speech-reco.md)  |
| mutants.plugin.**restoreStatus** | 安卓restore状态查询(Private) |                                       |



**所有插件的方法, 都可以在对应的 `mutants.plugin[pluginName]` 上直接使用.**

为了兼容好会计之前的调用方式, 每一个插件的包依旧支持独立使用 , 等好会计调整过后. 将不再提供.












