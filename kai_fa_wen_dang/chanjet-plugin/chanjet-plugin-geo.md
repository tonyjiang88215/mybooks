# 定位API  `chanjet-plugin-geo`

在mutants框架中, 提供定位相关的api , 只在chanjet平台上可用, 微信不提供此功能.

**不能脱离mutants框架单独使用.**



## 获取实例

```javascript
//通过mutants来获取插件实例
const plugin = mutants.plugin.geo;
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

2. #### displayNearby 根据位置显示周边

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
//获取插件实例
const plugin = mutants.plugin.geo;



/************** 获取当前位置 **************/
plugin.getLocation( (rs) => {
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
plugin.displayNearby( options , (rs) => {
  console.log(rs);
});
```



## mock数据

在浏览器环境中,可以通过mock数据来模拟返回结果 , 可以使用 `mutants.plugin.setMockData` 来设置mock数据.

具体参考如下:



### 模拟成功

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  GeoPlugin : {
    //获取当前位置mock数据
    getLocation : {
      status : 'success',
      data : {
        accuracy: 29,
        city: "010",
        latitude: 40.067496,
        location: "北京市海淀区永腾南路靠近用友软件园中区8D",
        locationTimestamp: 1461722019140,
        longitude: 116.236093
      }
    },
    
    //查看附近选择mock数据
    displayNearby : {
      status : 'success',
      data : {
        accuracy: 0,
        city: "010",
        latitude: 40.066948,
        location: "北京久瑞医疗科技有限公司",
        locationTimestamp: 1461722134777,
        longitude: 116.235596
      }
    }
    
  }
}

//设置mock数据
mutants.plugin.setMockData(mockData);
```



### 模拟失败

```javascript
const mockData = {
  //mock数据中,键名为插件的类名
  GeoPlugin : {
    getLocation : {
      status : 'failed',
      message : '网络异常,请稍后再试'
    },
    displayNearby : {
      status : 'failed',
      message : '网络异常,请稍后再试'
    }
  }

}

//设置mock数据
mutants.plugin.setMockData(mockData);
```



