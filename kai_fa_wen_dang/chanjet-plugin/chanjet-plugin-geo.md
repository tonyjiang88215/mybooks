# 定位API  `chanjet-plugin-geo`

提供定位相关的api , 只在chanjet平台上可用, 微信不提供此功能.



### 安装

```
npm install chanjet-plugin-geo
```



## API

1. #### getLocation 获取当前位置

   ##### 返回值

   ```javascript
   const result ={
     resultCode : 0,
     message : '',
     body : {
       data : {
     //待补充
       }
     }

   }
   ```

2. #### displayNearBy 根据位置显示周边

   ##### 参数

   - options `Object` 设置选项
     - longitude `string` 经度
     - latitude `string` 纬度
     - location `string` 位置信息
     - city `string` 当前城市
     - radius `number` 周边半径 , 默认值 500 (米) , 最小值100
   - callback `function` 执行完成后回调

   ​



## 用法

```javascript
//加载插件
import GeoPlugin from 'chanjet-plugin-geo'

//初始化  
let plugin = new GeoPlugin();


/************** 获取当前位置 **************/

 this.geoPlugin.getLocation( (rs) => {
   console.log(rs);
 });



/************** 查看附近 **************/

const options = {
  longitude : '',
  latitude : '',
  location : '',
  city : '',
  
};

//调用查看附近
this.geoPlugin.displayNearBy( options , (rs) => {
  console.log(rs);
});

```