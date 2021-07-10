# AIOT视频数据对接接口文档(V0.1)

## 组织关系绑定

1. ### **aiot平台分组与业务平台组织建立映射关系**

   基本信息：

   ```text
   接口名称：aiot组织查询
   接口描述：根据AppId和Secret查询aiot组织与业务系统绑定
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   http://ip:port/tripartite/queryGroupListByAppIdAndSecret
   请求方式：
   GET
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   | **名称** | **类型** | **必须** | **备注**    |
      | -------- | -------- | -------- | ----------- |
   | appId    | String   | true     | IOT鉴权ID   |
   | secret   | String   | true     | IOT鉴权密钥 |

   请求示例：

   https://ip:port/tripartite/queryGroupListByAppIdAndSecret?appId=%s&secret=%s

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   |   名称    |  类型  |                             备注                             |
      | :-------: | :----: | :----------------------------------------------------------: |
   | requestId | string |                            请求ID                            |
   |   code    | string |                           操作编码                           |
   |  message  | string |                       操作结果描述信息                       |
   |   data    | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详情 |
   |  └─list   | array  |                           数据集合                           |
   |    id     | string |                          iot组织id                           |
   |   name    | string |                         iot组织名称                          |

   正确返回示例：

   ```json
   {
   "requestId":"38cd4590051e4894bae7ca0e96bc583c",
   "code":"200",
   "message":"OK",
   "data":[
             {
             "name":"测试",
             "id":"AXb5stqosn_QL8fBuIxP"
             },
             {
             "name":"测试2",
             "id":"AXb5stqosn_QL8fBuIxP1"
             }
   		]
   }
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```



2. ### aiot平台设备与业务平台组织建立映射关系

   基本信息：

   ```text
   接口名称：aiot组织设备查询
   接口描述：根据绑定的iot组织Id分页查询所有设备与业务平台组织绑定
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   http://ip:port/tripartite/queryIpcameraListByGroupId
   请求方式：
   GET
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   | **名称** | **类型** | **必须** |          **备注**           |
      | :------: | :------: | :------: | :-------------------------: |
   |  appId   |  String  |   true   |          IOT鉴权ID          |
   |  secret  |  String  |   true   |         IOT鉴权密钥         |
   |   page   |   int    |   true   |            页数             |
   | pageSize |   int    |   true   |          每页大小           |
   | groupIds |  string  |   true   | 绑定的iot组织Id多个逗号分隔 |

   请求示例：

   https://ip:port/tripartite/queryIpcameraListByGroupId?appId=%s&secret=%s&groupIds=%s&page=%s&pageSize=%s

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   |      名称      |  类型  |                             备注                             |
      | :------------: | :----: | :----------------------------------------------------------: |
   |   requestId    | string |                            请求ID                            |
   |      code      | string |                           操作编码                           |
   |    message     | string |                       操作结果描述信息                       |
   |      data      | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详情 |
   |     └─list     | array  |                           数据集合                           |
   |    deviceId    | string |                          终端盒子id                          |
   |   deviceName   | string |                         终端盒子名称                         |
   |   ipCameraId   | string |                            设备id                            |
   |  ipCameraName  | string |                           设备名称                           |
   | ipCameraStatus | string |              设备状态 0 是删除 1 是正常 2 离线               |
   |      lat       | string |                             纬度                             |
   |      lon       | string |                             经度                             |
   |    └─total     | int64  |                           数据总数                           |

   正确返回示例：

   ```json
   {
       "requestId": "38cd4590051e4894bae7ca0e96bc583c",
       "code": "200",
       "message": "OK",
       "data": [
           {
               "deviceId": "测试",
               "deviceName": "AXb5stqosn_QL8fBuIxP",
               "ipCameraName": "仓库",
               "ipCameraId": "AXb5stqosn_QL8fBuIxP",
               "ipCameraStatus": "1",
               "lat": ""，"lon": ""
           },
           {
               "deviceId": "测试2",
               "deviceName": "AXb5stqosn_QL8fBuIxP1",
               "ipCameraName": "仓库1",
               "ipCameraId": "AXb5stqosn_QL8fBuIxP1",
               "ipCameraStatus": "2",
               "lat": ""，"lon": ""
           }
       ]
   }
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```



## 数据查询

### 设备基本信息

1. ####  根据摄像头ID查询单个摄像头信息

   基本信息：

   ```text
   接口名称：根据摄像头ID查询摄像头信息
   接口描述：查询直播,回播,AI直播地址,摄像头描述信息等
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   https://ip:port/tripartite/queryDeviceCameraInfoById
   请求方式：
   GET
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   |  **名称**  | **类型** | **必须** |  **备注**   |
      | :--------: | :------: | :------: | :---------: |
   |   appId    |  String  |   true   |  IOT鉴权ID  |
   |   secret   |  String  |   true   | IOT鉴权密钥 |
   | ipCameraId |  string  |   true   |  摄像头ID   |

   请求示例：

   https://ip:port/tripartite/queryDeviceCameraInfoById?appId=%s&secret=%s&ipCameraId=%s

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   |       名称       |  类型  | 备注                                                         |
      | :--------------: | :----: | :----------------------------------------------------------- |
   |    requestId     | string | 请求ID                                                       |
   |       code       | string | 操作编码                                                     |
   |     message      | string | 操作结果描述信息                                             |
   |       data       | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详情 |
   |     deviceId     | string | 终端盒子id                                                   |
   |       name       | string | 视频名称                                                     |
   |    ipCameraId    | string | 设备id                                                       |
   |    updateTime    |  long  | 更新时间 13位毫秒级时间戳                                    |
   |      status      | string | 设备状态 0 是删除 1 是正常 2 离线                            |
   |   deviceHostIp   | string | 设备内网IP地址                                               |
   | deviceStreamPort | string | 设备内网端口                                                 |
   |    streamUrl     | object | 流媒体对象                                                   |
   |     └─aiLive     | array  | ai视频直播地址目前分为http和wss两种协议提供flv流             |
   |  └─playbackUrl   | object | 视频历史查询地址；<br/>1.playbackUrlVideoBetweenPath 地址为获取视频m3u8文件片段时间范围,get请求。参数如下：<br/>kind=smartNvr&ipCameraId=AXPqqFvBpaE7QKW0JOrC&startTime=1615874400000&endTime=1615877999999;<br/>其中kind有两种类型smartNvr（直播）及ai（ai直播）两种类型，ipCameraId视频唯一标识id，startTime及endTime代表查询时间范围毫秒时间戳。<br/>2.playbackUrlM3u8Path地址为获取视频播放m3u8文件地址。get请求参数如下：<br/>startTime=1615874404000&endTime=1615876524000&ipCameraId=AXPqqFvBpaE7QKW0JOrC&kind=smartNvr；<br/>其中kind有两种类型smartNvr（直播）及ai（ai直播）两种类型，ipCameraId视频唯一标识id，startTime及endTime代表查询时间范围毫秒时间戳(即第一个地址获取的m3u8 片段时间戳范围)<br/><br/>注:回放地址属于动态地址有api接口动态更新; |
   |      └─live      | array  | 视频直播地址目前分为http和wss两种协议提供flv流               |

   正确返回示例：

   ```json
   {
   "requestId":"38cd4590051e4894bae7ca0e96bc583c",
   "code":"200",
   "message":"OK",
   "data":{
   "streamUrl":{
     "aiLive":[
     ],
     "playbackUrl":{
                     "playbackUrlVideoBetweenPath":"https://aa.bb.com:9443/20166/proxy/ipCameraVideoCollection/streamer/videoBetween",
               "playbackUrlM3u8Path":"https://aa.bb.com:9443/20166/proxy/ipCameraVideoCollection/streamer/getM3u8"
     },
     "live":[
     {
        "wssFlv":"wss://aa.bb.com:9443/ws_live/live_pull/AXb5stqosn_QL8fBuIxP_480_360.flv?app=live&pull_domain=rtmp://127.0.0.1:9240",
                  "httpFlv":"https://aa.bb.com:9443/live_pull/AXb5stqosn_QL8fBuIxP_480_360.flv?app=live&pull_domain=rtmp://127.0.0.1:9240"
     }
     ]
     },
     "name":"cam1",
     "ipCameraId":"AXb5stqosn_QL8fBuIxP",
     "updateTime":1621856191209,
     "deviceId":"4cfa68c0109524e5c84c7dee2e7ee3d1",
     "status":"1",
     "deviceHostIp":"192.168.3.104",
     "deviceStreamPort":"1936"
   }
   }
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```



2. ####  根据摄像头ID 批量查询

   基本信息：

   ```text
   接口名称：根据摄像头ID批量查询
   接口描述：根据多个摄像头id批量查询直播,回播,AI直播地址,摄像头描述信息等
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   https://ip:port/tripartite/queryDeviceCameraInfoByIds
   请求方式：
   GET
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   |  **名称**   | **类型** | **必须** |     **备注**      |
      | :---------: | :------: | :------: | :---------------: |
   |    appId    |  String  |   true   |     IOT鉴权ID     |
   |   secret    |  String  |   true   |    IOT鉴权密钥    |
   | ipCameraIds |  string  |   true   | 摄像头ID,逗号分隔 |

   请求示例：

   https://ip:port/tripartite/queryDeviceCameraInfoByIds?appId=%s&secret=%s&queryDeviceCameraInfoByIds=%s

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   |       名称       |  类型  | 备注                                                         |
      | :--------------: | :----: | :----------------------------------------------------------- |
   |    requestId     | string | 请求ID                                                       |
   |       code       | string | 操作编码                                                     |
   |     message      | string | 操作结果描述信息                                             |
   |       data       | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详情 |
   |      └─list      | array  | 数据集合                                                     |
   |     deviceId     | string | 终端盒子id                                                   |
   |       name       | string | 视频名称                                                     |
   |    ipCameraId    | string | 设备id                                                       |
   |    updateTime    |  long  | 更新时间 13位毫秒级时间戳                                    |
   |      status      | string | 设备状态 0 是删除 1 是正常 2 离线                            |
   |   deviceHostIp   | string | 设备内网IP地址                                               |
   | deviceStreamPort | string | 设备内网端口                                                 |
   |    streamUrl     | object | 流媒体对象                                                   |
   |     └─aiLive     | array  | ai视频直播地址目前分为http和wss两种协议提供flv流             |
   |  └─playbackUrl   | object | 视频历史查询地址；<br/>1.playbackUrlVideoBetweenPath 地址为获取视频m3u8文件片段时间范围,get请求。参数如下：<br/>kind=smartNvr&ipCameraId=AXPqqFvBpaE7QKW0JOrC&startTime=1615874400000&endTime=1615877999999;<br/>其中kind有两种类型smartNvr（直播）及ai（ai直播）两种类型，ipCameraId视频唯一标识id，startTime及endTime代表查询时间范围毫秒时间戳。<br/>2.playbackUrlM3u8Path地址为获取视频播放m3u8文件地址。get请求参数如下：<br/>startTime=1615874404000&endTime=1615876524000&ipCameraId=AXPqqFvBpaE7QKW0JOrC&kind=smartNvr；<br/>其中kind有两种类型smartNvr（直播）及ai（ai直播）两种类型，ipCameraId视频唯一标识id，startTime及endTime代表查询时间范围毫秒时间戳(即第一个地址获取的m3u8 片段时间戳范围)<br/><br/>注:回放地址属于动态地址有api接口动态更新; |
   |      └─live      | array  | 视频直播地址目前分为http和wss两种协议提供flv流               |

   正确返回示例：

   ```json
   {
   "requestId":"38cd4590051e4894bae7ca0e96bc583c",
   "code":"200",
   "message":"OK",
   "data":[{
   "streamUrl":{
     "aiLive":[
     ],
     "playbackUrl":{
                     "playbackUrlVideoBetweenPath":"https://aa.bb.com:9443/20166/proxy/ipCameraVideoCollection/streamer/videoBetween",
               "playbackUrlM3u8Path":"https://aa.bb.com:9443/20166/proxy/ipCameraVideoCollection/streamer/getM3u8"
     },
     "live":[
     {
        "wssFlv":"wss://aa.bb.com:9443/ws_live/live_pull/AXb5stqosn_QL8fBuIxP_480_360.flv?app=live&pull_domain=rtmp://127.0.0.1:9240",
                  "httpFlv":"https://aa.bb.com:9443/live_pull/AXb5stqosn_QL8fBuIxP_480_360.flv?app=live&pull_domain=rtmp://127.0.0.1:9240"
     }
     ]
     },
     "name":"cam1",
     "ipCameraId":"AXb5stqosn_QL8fBuIxP",
     "updateTime":1621856191209,
     "deviceId":"4cfa68c0109524e5c84c7dee2e7ee3d1",
     "status":"1",
     "deviceHostIp":"192.168.3.104",
     "deviceStreamPort":"1936"
   }
   }
     ]
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```



3. #### 根据设备ID查询设备下的所有摄像头信息

   基本信息：

   ```text
   接口名称：根据设备ID查询设备下所有摄像头信息
   接口描述：查询直播,回播,AI直播地址,摄像头描述信息等,返回数组
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   https://ip:port/tripartite/queryDeviceCameraInfoByDeviceId
   请求方式：
   GET
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   | **名称** | **类型** | **必须** |    **备注**    |
      | :------: | :------: | :------: | :------------: |
   |  appId   |  String  |   true   |   IOT鉴权ID    |
   |  secret  |  String  |   true   |  IOT鉴权密钥   |
   | deviceId |  string  |   true   | 设备(黑匣子)ID |

   请求示例：

   https://ip:port/tripartite/queryDeviceCameraInfoByDeviceId?appId=%s&secret=%s&deviceId=%s

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   |       名称       |  类型  | 备注                                                         |
      | :--------------: | :----: | :----------------------------------------------------------- |
   |    requestId     | string | 请求ID                                                       |
   |       code       | string | 操作编码                                                     |
   |     message      | string | 操作结果描述信息                                             |
   |       data       | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详情 |
   |      └─list      | array  | 数据集合                                                     |
   |     deviceId     | string | 终端盒子id                                                   |
   |       name       | string | 视频名称                                                     |
   |    ipCameraId    | string | 设备id                                                       |
   |    updateTime    |  long  | 更新时间 13位毫秒级时间戳                                    |
   |      status      | string | 设备状态 0 是删除 1 是正常 2 离线                            |
   |   deviceHostIp   | string | 设备内网IP地址                                               |
   | deviceStreamPort | string | 设备内网端口                                                 |
   |    streamUrl     | object | 流媒体对象                                                   |
   |     └─aiLive     | array  | ai视频直播地址目前分为http和wss两种协议提供flv流             |
   |  └─playbackUrl   | object | 视频历史查询地址；<br/>1.playbackUrlVideoBetweenPath 地址为获取视频m3u8文件片段时间范围,get请求。参数如下：<br/>kind=smartNvr&ipCameraId=AXPqqFvBpaE7QKW0JOrC&startTime=1615874400000&endTime=1615877999999;<br/>其中kind有两种类型smartNvr（直播）及ai（ai直播）两种类型，ipCameraId视频唯一标识id，startTime及endTime代表查询时间范围毫秒时间戳。<br/>2.playbackUrlM3u8Path地址为获取视频播放m3u8文件地址。get请求参数如下：<br/>startTime=1615874404000&endTime=1615876524000&ipCameraId=AXPqqFvBpaE7QKW0JOrC&kind=smartNvr；<br/>其中kind有两种类型smartNvr（直播）及ai（ai直播）两种类型，ipCameraId视频唯一标识id，startTime及endTime代表查询时间范围毫秒时间戳(即第一个地址获取的m3u8 片段时间戳范围)<br/><br/>注:回放地址属于动态地址有api接口动态更新; |
   |      └─live      | array  | 视频直播地址目前分为http和wss两种协议提供flv流               |

   正确返回示例：

   ```json
   {
   "requestId":"38cd4590051e4894bae7ca0e96bc583c",
   "code":"200",
   "message":"OK",
   "data":[{
   "streamUrl":{
     "aiLive":[
     ],
     "playbackUrl":{
                     "playbackUrlVideoBetweenPath":"https://aa.bb.com:9443/20166/proxy/ipCameraVideoCollection/streamer/videoBetween",
               "playbackUrlM3u8Path":"https://aa.bb.com:9443/20166/proxy/ipCameraVideoCollection/streamer/getM3u8"
     },
     "live":[
     {
        "wssFlv":"wss://aa.bb.com:9443/ws_live/live_pull/AXb5stqosn_QL8fBuIxP_480_360.flv?app=live&pull_domain=rtmp://127.0.0.1:9240",
                  "httpFlv":"https://aa.bb.com:9443/live_pull/AXb5stqosn_QL8fBuIxP_480_360.flv?app=live&pull_domain=rtmp://127.0.0.1:9240"
     }
     ]
     },
     "name":"cam1",
     "ipCameraId":"AXb5stqosn_QL8fBuIxP",
     "updateTime":1621856191209,
     "deviceId":"4cfa68c0109524e5c84c7dee2e7ee3d1",
     "status":"1",
     "deviceHostIp":"192.168.3.104",
     "deviceStreamPort":"1936"
   }
   }
     ]
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```

### ai快照信息

1. #### 查询ai类型

   基本信息：

   ```text
   接口名称：查询ai类型
   接口描述：据AppId和Secret查询ai类型。返回树结构json数据
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   https://ip:port/tripartite/queryAiType
   请求方式：
   GET
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   | **名称** | **类型** | **必须** | **备注**    |
      | -------- | -------- | -------- | ----------- |
   | appId    | String   | true     | IOT鉴权ID   |
   | secret   | String   | true     | IOT鉴权密钥 |

   请求示例：

   https://ip:port/tripartite/queryAiType?appId=%s&secret=%s

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   |   名称    |  类型  |                             备注                             |
      | :-------: | :----: | :----------------------------------------------------------: |
   | requestId | string |                            请求ID                            |
   |   code    | string |                           操作编码                           |
   |  message  | string |                       操作结果描述信息                       |
   |   data    | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详情 |
   |  └─list   | array  |                           数据集合                           |
   |  aiType   | string |            行为标识关键字 用于查询ai快照信息字段             |
   |   name    | string |               行为标识名称例如越界，未戴口罩等               |
   |    id     | string |                            唯一id                            |
   | parentId  | string |                            父节点                            |
   | children  | string |                         是否有子节点                         |

   正确返回示例：

   ```json
   {
         "requestId": "38cd4590051e4894bae7ca0e96bc583c",
          "code": "200",
          "message": "OK",
   "data": [
     {
       "name": "AI智能抓拍类型",
       "id": "0",
       "parentId": "-1",
       "aiType": "aiCapture",
       "children": [
         {
           "name": "视频智能分析",
           "children": [
             {
               "children": [],
               "aiType": "outBoundary",
               "name": "越界",
               "id": "6",
               "parentId": "1"
             }
           ],
           "id": "1",
           "aiType": "aiVideo",
           "parentId": "0"
         }
       ]
     }
   ]
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```



2. #### 查询api快照地址

   基本信息：

   ```text
   接口名称：查询ai快照地址
   接口描述：根据绑定组织id查询ai快照地址
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   https://ip:port/tripartite/queryProxyCloudDomainByGroupId
   请求方式：
   GET
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   | **名称** | **类型** | **必须** | **备注**           |
      | -------- | -------- | -------- | ------------------ |
   | appId    | String   | true     | IOT鉴权ID          |
   | secret   | String   | true     | IOT鉴权密钥        |
   | groupId  | String   | true     | 绑定aiot平台组织Id |

   请求示例：

   https://ip:port/tripartite/queryProxyCloudDomainByGroupId?appId=%s&secret=%s&groupId=%s

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   |   名称    |  类型  |                             备注                             |
      | :-------: | :----: | :----------------------------------------------------------: |
   | requestId | string |                            请求ID                            |
   |   code    | string |                           操作编码                           |
   |  message  | string |                       操作结果描述信息                       |
   |   data    | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详 |

   正确返回示例：

   ```json
    {
         "requestId": "38cd4590051e4894bae7ca0e96bc583c",
          "code": "200",
          "message": "OK",
          "data": "xxxxx"
   }
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```



3. #### 根据组织查询AI抓拍信息

   基本信息：

   ```text
   接口名称：查询快照信息
   接口描述：根据组织ID分页查询快照信息
   注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
   请求地址：
   https://快照地址/snapshot/pageList
   请求方式：
    POST
   请求头：
   ```

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   请求参数说明：

   | **名称**  | **类型** | **必须** | **备注**                   |
      | --------- | -------- | -------- | -------------------------- |
   | startTime | long     | true     | 开始时间 13位毫秒时间戳    |
   | endTime   | long     | true     | 结束时间 13位毫秒时间戳    |
   | treeCode  | String   | false    | 组织ID                     |
   | sensorIds | array    | false    | 摄像头ID集合               |
   | types     | array    | true     | AI抓拍类型集合根据参数决定 |
   | page      | Int      | true     | 页码                       |
   | pageSize  | Int      | true     | 分页大小                   |

   请求示例：

   ```json
   https://ip:port/snapshot/pageList
   {
   
   "startTime": 0,
   
   "endTime": 1622167455108,
   
   "deptIds": ["136438"],
   
   "sensorIds": [],
   
   "types": ["strangers","noMask","noHat","noGlove","smoking","hiddenCamera","human","noClothes"],
   
   "page": 1,
   
   "pageSize": 20
   
   }
   
   
   ```

   返回参数头：

   |     名称     |  类型  | 必填 |      默认值      |              备注              |
   | :----------: | :----: | :--: | :--------------: | :----------------------------: |
   | Content-Type | string | true | application/json | 指定参数类型为application/json |

   返回参数说明：

   | 名称            |  类型  |        备注        |
      | :-------------- | :----: | :----------------: |
   | requestId       | string |       请求ID       |
   | code            | string |      操作编码      |
   | message         | string |  操作结果描述信息  |
   | data            | object |      数据集合      |
   | pageSize        |  int   |      每页大小      |
   | pageCount       |  int   |        页数        |
   | totalCount      |  int   |       总行数       |
   | list            | array  |      数据集合      |
   | └─deptId        | string |   业务平台组织id   |
   | └─stImgDesc     | string |  快照抓拍信息描述  |
   | └─updateTime    |  long  |    快照更新时间    |
   | └─deviceId      | string |   智能设备终端Id   |
   | └─sensorId      | string |      摄像头Id      |
   | └─aiSceneType   | string |       ai场景       |
   | └─createTime    |  long  |    快照创建时间    |
   | └─deviceGroupId | string | 智能设备终端分组Id |
   | └─aiType        | string |       ai类型       |
   | └─thumbnailPath | string |  快照缩略图片地址  |
   | originalPath    | string |  快照原始图片地址  |
   | └─id            | string |       快照id       |
   | └─treeCode      | string |     组织id集合     |
   | └─mp4Path       | string |   快照短视频地址   |
   | └─createDate    | string |    快照创建时间    |

   正确返回示例：

   ```json
   {
       "requestId": "9507732313fd4779b0429e49c2488004",
       "code": "success",
       "message": "success",
       "data": {
   		page": 1,
           "pageSize": 20,
           "pageCount": 217,
           "totalCount": 4323,
           "list": [
               {
                   "deptId": "201",
                   "stImgDesc":"{\"PicTime\":\"2021-07-01 11:39:01\",\"PicPath\":\"/data/historyVideo/34dc9e8bf18761c340c1b513f653dbf9/ai_snapshot/wear_kitchen/2021-07-01/11-39-01_32.jpg\",\"ROIS\":[{\"RoiText\":\"Trackxperson^Id_883-\>Yolovx^未戴帽子\",\"Bbox\":\"191,207,69,146\"}]}",
                   "updateTime": "1625139551671",
                   "deviceId": "8b2c18da374c5798f22944fb0e71563a",                                
                   "sensorId": "34dc9e8bf18761c340c1b513f653dbf9",
                   "aiSceneType": "",
                   "createTime": "1625139541000",
                   "deviceGroupId": "",
                   
                   "aiType": "noHat",
                  
                   "thumbnailPath": "https://aiotshidiandata.shikongshuzhi.com:9443/snap_receive_api/snap/load?path=icon/2021-07-01/325d765b3013f699de283aeed48745ed.jpg",
                    
                   "id": "325d765b3013f699de283aeed48745ed",
                  
                   "originalPath": "https://aiotshidiandata.shikongshuzhi.com:9443/snap_receive_api/snap/load?path=image/2021-07-01/325d765b3013f699de283aeed48745ed.jpg",
                   "treeCode": "0,100,101,107,201",
                   "mp4Path": "https://aiotshidiandata.shikongshuzhi.com:9443/snap_receive_api/snap/load?path=ts/2021-07-01/325d765b3013f699de283aeed48745ed.mp4",
                   "createDate": "2021-07-01"
               }
   ]
       }
   }
   ```

   错误返回示例:

   ```json
   {
   
      "requestId": "6422806bf92941f79ec78f9bba434c5b",
   
      "code": "error",
   
      "message": "系统错误",
   
      "data": null
   
   }
   ```



4. #### 删除AI快照信息

基本信息：

```text
接口名称：删除快照信息
接口描述：根据快照id 集合删除快照信息
注：appId 和secret需要申请，调用方需向服务提供方申请appId 和secret。
请求地址：
https://快照地址/tripartite/queryAiType
请求方式：
GET
请求头：
```

|     名称     |  类型  | 必填 |      默认值      |              备注              |
| :----------: | :----: | :--: | :--------------: | :----------------------------: |
| Content-Type | string | true | application/json | 指定参数类型为application/json |

请求参数说明：

| **名称** | **类型** | **必须** | **备注**               |
| -------- | -------- | -------- | ---------------------- |
| idList   | string   | true     | 快照id以逗号分隔字符串 |

请求示例：

https://ip:port/snapshot/deleteById?idList=%s

返回参数头：

|     名称     |  类型  | 必填 |      默认值      |              备注              |
| :----------: | :----: | :--: | :--------------: | :----------------------------: |
| Content-Type | string | true | application/json | 指定参数类型为application/json |

返回参数说明：

|   名称    |  类型  |                             备注                             |
| :-------: | :----: | :----------------------------------------------------------: |
| requestId | string |                            请求ID                            |
|   code    | string |                           操作编码                           |
|  message  | string |                       操作结果描述信息                       |
|   data    | string | 返回的数据，如果操作成功返回本次操作的批次操作代码，如果失败返回有错误的数据详 |

正确返回示例：

```json
 {
      "requestId": "38cd4590051e4894bae7ca0e96bc583c",
       "code": "200",
       "message": "OK",
       "data": null
}
```

错误返回示例:

```json
{

   "requestId": "6422806bf92941f79ec78f9bba434c5b",

   "code": "error",

   "message": "系统错误",

   "data": null

}
```





