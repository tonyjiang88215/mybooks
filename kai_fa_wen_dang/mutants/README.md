Mutants

作为Mutants框架的入口,内嵌了 chanjet-env-check 环境检测包 , 对不同平台的nativeSDK进行统一预处理.



安装

    npm install mutants



用法

    import mutants from 'chanjet-mutants'
    
    //应用
    class Application{
      constructor(){
        //some code...
      }
    
      startUp(){
      	//some code....
      }
    }
    
    mutants.config({
      plugins : [
        //这里将要使用的插件预先定义,以便对微信处理预授权
      	require('chanjet-plugin-share').default,
        require('chanjet-plugin-sms').default
      ],
      auth : {
        //暂时没有
        chanjet : {},
        //详见微信开发文档,这里只是对微信的config进行封装
        weixin : {
          debug : false,
          appId : '',
          timestamp : '',
          nonceStr : '',
          signature : ''
        }
      }
    });
    
    //监听ready方法,成功后启动应用
    mutants.ready(function(){
      new Application().startUp();
    })
    



环境检测

    import mutants from 'chanjet-mutants'
    
    /*
    mutants封装了chanjet-env-check对象,可以快速获取当前环境,无需在引入chanjet-env-check包,详见接口文档
    */
    
    //当前平台
    console.log(mutants.platform);
    //当前系统或设备
    console.log(mutants.os);
    //当前浏览器
    console.log(mutants.browser);
    
    //可以通过constant来判断
    
    //判断是否是chanjet平台
    mutants.platform == mutants.constant.platform.chanjet
    //判断是否是ios操作系统
    mutants.os == mutants.constant.os.ios
    //判断是否是chrome浏览器
    mutants.browser == mutants.constant.browser.chrome
