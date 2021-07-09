# iot-plugin
#### 介绍
本文主要介绍插件的开发流程规范其中包括插件实现restful的接口、及必要的功能介绍。
#### 运行环境
插件运行环境基于linux操作系统，例如centos 7.0以上版本及ubuntu操作系统18.0及以上。
#### 插件命名规范
插件命名遵循驼峰命名都是以 iot-plugin- 开头 插件名称结尾 例如：iot-plugin-插件名称
#### 插件部署目录结构
    插件目录名称
     ｜--conf
     ｜--lib
     ｜--startup.sh
     ｜--shutdown.sh
     ｜--cover.png
     ｜--conf.sh
     ｜--plugin.desc
     ｜--assembly
     ｜--port.txt

    插件目录名称为插件根目录, 其下有conf，lib文件夹及startup.sh，shutdown.sh 文件。名称是以插件唯一标识id_插件名称组合而成。
    1.conf文件夹为配置文件存储目录。目前分为2类文件:系统配置文件及日志配置文件。
    2.lib 文件夹为一些插件编译的代码包
    3.startup.sh及shutdown.sh 为插件的启动和暂停脚本。
    4.cover.png 插件封面图片
    5.conf.sh 用于终端IOT-Platform-Iot-Client管理插件服务与插件系统关键配置信息同步操作shell 脚本。
    6.assembly 插件组件存储文件夹
    7.port.txt 插件端口
    8.plugin.desc 插件说明结构如下：
     {"pluginId" : "ipCameraVideoCollection","pluginName" : "视频采集", "version" : "1.0.3","show":true}
     说明： pluginId  插件id,pluginName 插件名称,version 插件版本，show 是否显示

#### 实现接口说明
插件必须实现接口如下：

#### 必须实现功能如下
1.插件服务定时将心跳信息写入磁盘文件。

    插件服务启动需要定时默认时间间隔10s在插件根目录下写入文件heart.txt.格式如下：
    time,port,status
     说明：time 代表写入当前时间戳，port服务端口,status 插件状态
2.插件需要实现反向代理用于代理组件的api接口

















