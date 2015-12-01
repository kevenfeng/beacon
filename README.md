
# 前端终端接口文档
android和ios接口实现方法全部使用prompt。为了统一调用前端调用终端接口全部使用异步的方式

### 前端调用终端接口实现方案
>>前端将参数以`beacon://[setTitle-{"callbackId":"1448952151037|1","option":"{'title':'灯塔-指引钱途'}"}]`的形式放入prompt中传给终端

>>终端处理好对应操作以后调用前端webview全局函数`AppCallback`，将callbackId和要返回的参数传入函数中

>>AppCallback(callbackId,option);

### 终端调用前端函数实现方案

>>终端调前端函数时统一调用前端ReqWeb函数 ReqWeb(key,value)
>>例如终端需要调用方法来改变前端的字体大小的时候
```javascript
ReqWeb("adjustFontSize",{size:"big"})
```

### 前端调用终端接口有

**setTitle**

>前端调用方式： 
```javascript
beaconApi.exec("setTitle",{title:"灯塔-指引钱途"},function(data){
       //回调函数，前端获取data后做相应逻辑
});
```
>函数作用：在终端界面设置title

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| title | string | 表示title具体内容 |

>返回数据：data = {status:0}
>>对status的说明：

>>当 `status === 0` &nbsp;&nbsp;时，表示设置标题成功；

>>当 `status === -1` &nbsp;&nbsp;时，表示设置标题失败；


**closeWindow**

>前端调用方式： 
```javascript
beaconApi.exec("closeWindow",{},function(data){
       //回调函数，前端获取data后得到是否关闭成功
});
```
>函数作用：关闭终端当前界面

>输入参数：无

>返回数据：data = {status:0}
>>对status的说明：

>>当 `status === 0` &nbsp;&nbsp;时，表示关闭成功；

>>当 `status === -1` &nbsp;&nbsp;时，表示关闭失败；

**setDiscoveryPageType**

>前端调用方式： 
```javascript
beaconApi.exec("setDiscoveryPageType",{pagetype：5},function(data){
       //回调函数，前端获取data后得到是否设置成功
});
```
>函数作用：告诉终端当前页面属于什么页面

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| pagetype | int | 表示页面类型 |

>>pagetype：
>>当 `pagetype === 5` &nbsp;&nbsp;时，表示从市场情报页面进入新闻页面；

>>当 `status === 6` &nbsp;&nbsp;时，表示从智能选股页面进入主题页面；
>返回数据：data = {status:0}
>>对status的说明：

>>当 `status === 0` &nbsp;&nbsp;时，表示设置成功；

>>当 `status === -1` &nbsp;&nbsp;时，表示设置失败；


**reloadUrl**

>前端调用方式： 
```javascript
beaconApi.exec("reloadUrl",{},function(data){
       //回调函数，前端获取data后得到是否reload成功
});
```
>函数作用：reload当前h5页面

>输入参数：无
>返回数据：data = {status:0}
>>对status的说明：

>>当 `status === 0` &nbsp;&nbsp;时，表示load成功；

>>当 `status === -1` &nbsp;&nbsp;时，表示load失败；

**downloadFile**

>前端调用方式： 
```javascript
beaconApi.exec("downloadFile",{url：""},function(data){
       //回调函数，前端获取data后得到是否发布下载命令成功
});
```
>函数作用：下载文件

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| url | string | 表示下载地址 |

>返回数据：data = {status:0}
>>对status的说明：

>>当 `status === 0` &nbsp;&nbsp;时，表示下载命令成功；

>>当 `status === -1` &nbsp;&nbsp;时，表示下载命令失败；


**openPdfFileBySystem**

>前端调用方式： 
```javascript
beaconApi.exec("openPdfFileBySystem",{url：""},function(data){
       //回调函数，前端获取data后得到是否打开成功
});
```
>函数作用：打开pdf文件

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| url | string | 表示下载地址 |

>返回数据：data = {status:0}
>>对status的说明：

>>当 `status === 0` &nbsp;&nbsp;时，表示打开成功；

>>当 `status === -1` &nbsp;&nbsp;时，表示打开失败；


**isPdfFileExists**

>前端调用方式： 
```javascript
beaconApi.exec("isPdfFileExists",{url：""},function(data){
       //回调函数，前端获取data后得到是否存在
});
```
>函数作用：是否存在该pdf

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| url | string | 表示下载地址 |

>返回数据：data = {status:0}
>>对status的说明：

>>当 `status === 0` &nbsp;&nbsp;时，表示存在；

>>当 `status === -1` &nbsp;&nbsp;时，表示不存在；


**getAccountInfo**

>前端调用方式： 
```javascript
beaconApi.exec("getAccountInfo",{},function(data){
       //回调函数，前端获取data后得到用户身份态
});
```
>函数作用：获取用户身份态

>输入参数：无

>返回数据：
>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| dtid | string | 表示id |
>| dtticket | string | 表示ticket |
>| DT-UA | string | 表示DT-UA |
>| DT-GUID | string | 表示DT-GUID|

### 终端调用前端接口有

**adjustFontSize**

>终端调用方式： 
```javascript
ReqWeb("adjustFontSize",{size:"big"})
```

>前端设置处理函数方式：
 ```javascript
lisenNative('adjustFontSize',function (value) {
    //通过value来判断如何改变字体大小
});
 ```
 
>函数作用：终端修改页面字体大小

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| size | string | 表示字体大小 |

>返回数据：value = {size:"big"}
>>对status的说明：

>>当 `size === big` &nbsp;&nbsp;时，表示设置字体放大；

>>当 `size === small` &nbsp;&nbsp;时，表示设置字体缩小；

**updateDownloadProgress**

>终端调用方式： 
```javascript
ReqWeb("updateDownloadProgress",{url:"http://***.pdf",progress:0.8})
```

>前端设置处理函数方式：
 ```javascript
lisenNative('updateDownloadProgress',function (value) {
    //通过value来获取进度条进度
});
 ```
 
>函数作用：获取下载文件进度条信息

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| url | string | 表示下载的文件的地址 |
>| progress | float | 表示下载进度 |

>返回数据：value = {url:"http://***.pdf",progress:0.8}

**downloadComplete**

>终端调用方式： 
```javascript
ReqWeb("downloadComplete",{url:"http://***.pdf",success:true})
```

>前端设置处理函数方式：
 ```javascript
lisenNative('downloadComplete',function (value) {
    //通过value来获取是否下载成功
});
 ```
 
>函数作用：获取下载文件进度条信息

>输入参数：

>| 参数  | 数据类型 | 描述 |
>| ------------- | ------------- | ------------- |
>| url | string | 表示下载的文件的地址 |
>| success | bool | 表示是否下载成功 |

>返回数据：value = {url:"http://***.pdf",success:true}
