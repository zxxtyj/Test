# iot-plugin-ipCameraVideoCollection

#### 介绍
插件主要服务与终端信息采集,处理。
#### 软件架构
软件架构说明
#### 安装教程
插件基于java语言编写依赖与spring boot体系框架，使用前需要jdk1.8环境编译。使用mvn插件打包部署即可。
#### 使用说明
#### 接口说明

一、插件设备管理接口

1.添加设备

       URL: http://ip:port/device/createDevice
       Type: POST
       Content-Type: application/json; charset=utf-8
       Description: 添加
       Request-parameters:

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|name|string|设备名称|true|
|username|string|设备账号|false|
|password|string|设备密码|false|
|cameraIp|string|设备ip|true|
|rtspPort|string|设备rtsp 端口 默认554|false|
|rtspUrl|string|设备取流地址|true|



       Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

           说明：
            1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
            2.data 响应的数据对象为空。


2.更新设备

       URL: http://ip:port/device/updateDevice?id=xx
       Type: PUT
       Content-Type: application/json; charset=utf-8
       Description: 更新
       Request-parameters:
|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|id|string|设备id|true|
|name|string|设备名称|false|
|username|string|设备账号|false|
|password|string|设备密码|false|
|cameraIp|string|设备ip|false|
|rtspPort|string|设备rtsp 端口 默认554|false|
|rtspUrl|string|设备取流地址|false|

        Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

         说明：
           1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
           2.data 响应的数据对象为空。

3.查询设备列表接口

        URL: http://ip:port/device/getPageListDevice?name=xx&page=1&pageSize=123
        Type: GET
        Content-Type: application/x-www-form-urlencoded;charset=utf-8
        Description: 获取任务列表

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|name|string|插件名称|false|
|page|int|页数|true|
|pageSize|int|每页大小|true|

          Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|Array|响应的数据集合|

          说明：
            1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
            2.data 响应的数据对象集合结构如下：
              {
                total 数据总行数，
                list 数据集合对象
                   └─name	string	设备名称
                   └─id	string 设备id
                   └─username	string	设备账号
                   └─password	string	设备密码
                   └─cameraIp	string	设备ip
                   └─rtspPort	string	设备rtsp端口
                   └─rtspUrl	string	设备取流地址
                   └─createTime	int64	创建时间
                   └─updateTime	int64	更新时间
              }
4.通过id查询

         URL: http://ip:port/device/getDeviceById?id=xxx
         Type: GET
         Content-Type: application/x-www-form-urlencoded;charset=utf-8
         Description: 获取任务列表

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|id|string|插件id|true|

             Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|object|响应的数据对象|

          说明：
            1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
            2.data 响应的数据对象集合结构如下：
                {
                  └─name	string	设备名称
                  └─id	string 设备id
                  └─username	string	设备账号
                  └─password	string	设备密码
                  └─cameraIp	string	设备ip
                  └─rtspPort	string	设备rtsp端口
                  └─rtspUrl	string	设备取流地址
                  └─createTime	int64	创建时间
                  └─updateTime	int64	更新时间
                }


5.通过id删除

         URL: http://ip:port/device/deleteDevice
         Type: delete
         Content-Type: application/x-www-form-urlencoded;charset=utf-8
         Description: 删除
         Request-parameters:

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|ids|array|任务id数组集合|true|

           Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

          说明：
            1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
            2.data 响应的数据对象为空。



二、插件任务接口

1.添加任务

       URL: http://ip:port/task/createTask
       Type: POST
       Content-Type: application/json; charset=utf-8
       Description: 添加
       Request-parameters:

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|name|string|任务名称|true|
|deviceId|string|设备id|true|
|config|string|任务配置信息|true|
|gstCmd|string|cmd 任务执行命令|false|

       Response-fields:
|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

       说明：
        1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
        2.data 响应的数据对象为空。

2.更新任务接口

      URL: http://ip:port/task/updateTask?id=xx
      Type: PUT
      Content-Type: application/json; charset=utf-8
      Description: 更新
      Request-parameters:

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|id|string|id|true|
|name|string|任务名称|false|
|deviceId|string|设备id|false|
|config|string|任务配置信息|false|
|gstCmd|string|cmd 任务执行命令|false|

      注：任务配置信息字段详见任务配置信息。

     Response-fields:
|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|string|响应的数据|

     说明：
      1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
      2.data 响应的数据对象为空。

3.任务启动接口

       URL: http://ip:port/task/startTask
       Type: POST
       Content-Type: application/json; charset=utf-8
       Description: 任务操作
       Request-parameters:
|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|ids|array|id集合|true|

       Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

      说明：
       1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
       2.data 响应的数据对象为空。

4.任务停止接口

         URL: http://ip:port/task/stopTask
         Type: POST
         Content-Type: application/json; charset=utf-8
         Description: 任务停止
         Request-parameters:
|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|ids|array|id集合|true|

         Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

        说明：
         1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
         2.data 响应的数据对象为空。

5.获取任务列表接口

       URL: http://ip:port/task/getPageListTask?deviceId=e223&page=1&pageSize=123
       Type: GET
       Content-Type: application/x-www-form-urlencoded;charset=utf-8
       Description: 获取任务列表

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|deviceId|string|设备id|false|
|page|int|页数|true|
|pageSize|int|每页大小|true|

       Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|Array|响应的数据集合|

       说明：
         1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
         2.data 响应的数据对象集合结构如下：
           {
             total 数据总行数，
             list 数据集合对象
                └─name	string	任务名称
                └─id	string	任务id
                └─deviceId	string	设备id
                └─config	string	任务配置信息
                └─status	string	任务状态默认是停止 0 是停止 1 运行中
                └─createTime	int64	创建时间
                └─updateTime	int64	更新时间
                └─gstCmd	String	cmd 任务执行命令
                └─type	string	任务类型
                └─ratio	string	任务分辨率
           }


6.删除任务接口

        URL: http://ip:port/v1/task/deleteTask
        Type: delete
        Content-Type: application/x-www-form-urlencoded;charset=utf-8
        Description: 删除
        Request-parameters:

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|ids|array|任务id数组集合|true|

        Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

       说明：
         1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
         2.data 响应的数据对象为空。

三、流媒体接口

1.回放获取m3u8接口

      URL: http://ip:port/streamer/getM3u8?startTime=1&endTime=12&&deviceId=xx&suffix=1&kind=xx
      Type: POST
      Content-Type: application/json; charset=utf-8
      Description: 回放接口

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|startTime|string|开始时间|true|
|endTime|string|结束时间|true|
|deviceId|string|设备id|true|
|suffix|string|是否添加参数后缀 1 添加 0 是否|false|
|kind|string|视频类型 分为smartNvr和ai|true|

      Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|string|响应的数据|

       说明：
         1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
         2.data 响应信息为空。
         3.响应m3u8流文本信息

2.获取视频流接口

        URL: http://ip:port/live/{appcationId}/{kind}/{ts}/{date}/{smart}/{name}
        Type: GET
        Content-Type: application/json; charset=utf-8
        Description: 回放接口

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|appcationId|string|设备id|true|
|kind|string|类型|true|
|ts|string|ts目录名称|true|
|date|string|日期目录|false|
|smart|string|视频类型 分为smartNvr和ai|true|
|name|string|视频文件名称|true|

        Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|void|响应的数据|

         说明：
           1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
           2.data 响应信息为空。
           3.响应视频文件流

3.获取视频区间接口

          URL: http://ip:port/streamer/getM3u8?startTime=1&endTime=12&&deviceId=xx&kind=xx
          Type: GET
          Content-Type: application/json; charset=utf-8
          Description: 获取视频区间

|Parameter|Type|Description|Required|
|--:|--:|--:|--:|
|startTime|string|开始时间|true|
|endTime|string|结束时间|true|
|deviceId|string|设备id|true|
|kind|string|视频类型 分为smartNvr和ai|true|

          Response-fields:

|Field|Type|Description|
|--:|--:|--:|
|requestId|string|响应自动生成的id|
|code|string|响应code|
|message|string|响应的消息|
|version|string|版本|
|data|Array|响应的视频流数据时间段集合|

           说明：
             1.code 响应的状态 200 代表请求成功 400代表请求参数错误 404 接口不存在 500 服务异常 403  资源不可用 无权限访问
             2.data 响应的数据对象集合结构如下：
                {
                  list 数据集合对象
                     └─startTime	long	开始时间
                     └─endTime	long	结束时间
                }
