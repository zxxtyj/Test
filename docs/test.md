# iot-plugin-ipCameraVideoCollection

#### 介绍
插件主要服务与终端信息收集，处理和云端信息同步等功能。对外发布数据api接口。
#### 软件架构
软件架构说明
#### 安装教程
插件基于java语言编写依赖与spring boot体系框架，使用前需要jdk1.8环境编译。使用mvn插件打包部署即可。
#### 使用说明
#### 功能描述 ：
    1.设备摄像头的管理创建、删除、修改删除等操作。
    2.视频直播采集任务创建、删除、修改、启动、暂停、视频存储等操作。
    3.视频ai直播任务创建、删除、修改、启动、暂停、视频存储，抓拍快照存储等操作。
    3.视屏预览及历史回放的查看
    4.删除一定时间范围内数据定任务定时器
    5.定时检测任务重启操作。
    6.服务启动时自动挂起上一次已启动采集任务。
    7.采集任务存活状态监控失败自动挂起。
    8.定时生成文件视频索引。
    9.定时同步心跳信息和同步配置信息到云端存储。

#### 配置文件描述 ：
    插件配置文件为两类：
    系统配置文件和任务配置文件。
     1.系统配置文件 bootstrap.properties 配置内容如下：
       #保留视频文件天数 目前最大值不超过15天
       delete.file.days=3
       #服务启动是否重启任务开关 true 开启 false关闭
       smartNvr.task.restart=true
     2.日志配置文件：
     <configuration scan="scan" scanPeriod="10 seconds" debug="false">
         <springProperty scope="context" name="app_name" source="spring.application.name"/>
         <include resource="org/springframework/boot/logging/logback/defaults.xml"/>
         <include resource="org/springframework/boot/logging/logback/console-appender.xml"/>
         <jmxConfigurator/>
         <property name="logName" value="logs/plugin-ipCameraVideoCollection"/>
         <appender name="rollingFile" class="ch.qos.logback.core.rolling.RollingFileAppender">
             <file>${logName}.log</file>
             <encoder>
                 <pattern>%d{yyyy-MM-dd} %d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
             </encoder>
             <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
                 <fileNamePattern>${logName}.%d{yyyy-MM-dd}.%i.log</fileNamePattern>
                 <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                     <maxFileSize>2MB</maxFileSize>
                 </timeBasedFileNamingAndTriggeringPolicy>
                 <MaxHistory>1</MaxHistory>
             </rollingPolicy>
         </appender>
         <root level="INFO">
             <appender-ref ref="rollingFile"/>
             <appender-ref ref="CONSOLE"/>
         </root>
     </configuration>


##### shell 脚本文件 conf.sh
     插件更目录下存在conf.sh文件用于管里插件IOT-Platform-Iot-Client服务与插件配置信息同步替换操作。
     例如：当IOT-Platform-Iot-Client 端修改插件配置调用脚本更新当前插件配置文件操作。

#### plugin.desc 插件信息文件
    插件描述信息文件主要介绍插件的id和名字及版本操作

#### 任务配置模版文件 taskDefaultConfig
    任务配置模版文件主要用于任务创建时默认值的模版操作。
