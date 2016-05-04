# 分享API `chanjet-plugin-share`

在mutants框架中, 提供分享到媒体平台api.

**不能脱离mutants框架单独使用.**



## 获取实例

```javascript
//通过mutants来获取插件实例
const plugin = mutants.plugin.share;
```





### 用法

``` javascript
const plugin = mutants.plugin.share;

//也可以在异步处理中动态修改分享内容,但是在微信中,不确定用户分享时间,所以存在问题
plugin.shareData = {
  title : '分享标题',
  content : '分享内容',
  img : '分享显示的图片',
  url : '分享跳转的地址',
  
  //分享成功的回调
  success : function(){},
  //分享失败的回调
  failed : function(){},
  //分享被取消的回调
  cancel : function(){}
  
}
```