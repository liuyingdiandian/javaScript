# mapOffline
配置离线地图, 百度地图@3.0
----------

#### 工作中用到离线地图的需求，所以就花了点时间总结一下具体配置过程：

##### 1、拿到API主文件：
  * 下载最新的api文件，不需要申请ak，地址：http://api.map.baidu.com/api?v=2.0：
  * 打开框框内的地址，即可看到主文件内容， 格式化一下， 复制到新建 apiv2.0.min.js文件中
  * 格式化工具： http://www.bejson.com/jshtml_format/

##### 2、改造apiv2.0.min.js：
  * 去掉ak验证： 搜索charset = 'utf-8'，添加:
    ```javascript
      if (/^http/.test(a)) return;
    ```
  
  * 不再使用外部资源，引入本地工具资源：
      * 搜索 domain.main_domain_cdn.baidu[0]，找到使用它定义的z.ma，修改为z.ma = '';
      
  * 加载模块短路处理：
    搜索 &mod=，替换为本地模块
    
  * 创建本地工具资源文件getmodules2.0.js
    在这里面放API需要调用的模块，上面打印的数组a里面是需要请求的模块，打印出来，通过下面方式获取，放到getmodules2.0.js,例如 canvablepath_lf2t4w, 通过 http://api0.map.bdimg.com/getmodules?v=2.0&t=20140707&mod=canvablepath_lf2t4w下载。更改后面的模块名即可下载！
   
  * 下载离线瓦片
  
  * 修改获取图片的地址为本地：
      * 在apiv2.0.min.js中找到相关代码，搜索 getTilesUrl，同上, 找到后修改。
      
    <br>  
  好啦， 在本地起个加载瓦片的服务就可以用啦~~~
    <hr>
  

#### 附： 
 <br>
  百度自定义个性化样式地址， 个性化编辑器：  http://lbsyun.baidu.com/customv2/editor/64273224b543444023195598a5282bbb
  百度地图开放平台： http://lbsyun.baidu.com/jsdemo.htm#canvaslayer 


