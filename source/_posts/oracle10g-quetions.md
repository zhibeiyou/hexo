---
title: oracle10g 监听服务启动不了
date: 2018-05-06 17:47:11
tags: [oracle10g,oracle基础]
categories: oracle数据库
keywords: [oracle10g,oracle基础]
---
关于解决oracle10g监听服务启动不了问题记录
 <!--more-->
 
 ### oracle10g连接远程数据库
 oracle10g连接远程数据库失败报错信息如下
 `The Network Adapter could not establish the connection` 
 经排查，错误原因是由E:\Oracle10gXEUniv\app\oracle\product\10.2.0\server\NETWORK\ADMIN(具体为你的oracle10g安装位置)下的listener.ora和tnsnames.ora中的host值没有设置为要连的远程ip地址。在这里，远程我只连接本地，将host值修改为127.0.0.1即可。
 **注意：如果你的listener.ora文件中没有XE实例，你需要对照下面的修改前的该文件内容**

 ### host值修改后报出ORA-12514: TNS
 ORA-12514: TNS：监听程序当前无法识别连接描述符中请求的服务
 再次修改listener.ora文件，修改前该文件内容为:
 ```SID_LIST_LISTENER =
 (SID_LIST =
 (SID_DESC =
 (SID_NAME = PLSExtProc)
 (ORACLE_HOME = E:\Oracle10gXEUniv\app\oracle\product\10.2.0\server)
 (PROGRAM = extproc)
 )
 (SID_DESC =
 (SID_NAME = CLRExtProc)
 (ORACLE_HOME = E:\Oracle10gXEUniv\app\oracle\product\10.2.0\server)
 (PROGRAM = extproc)
 )
 )
 
 LISTENER =
 (DESCRIPTION_LIST =
 (DESCRIPTION =
 (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC_FOR_XE))
 (ADDRESS = (PROTOCOL = TCP)(HOST = 127.0.0.1)(PORT = 1521))
 )
 )
 
 DEFAULT_SERVICE_LISTENER = (XE)```
 
 修改的方式是：再在该文件中添加一个需要连接的数据库实例的描述，就是添加一个SID_DESC，我自己连接的数据库实例是XE，添加后的文件内容为：
 ```
 SID_LIST_LISTENER =
 (SID_LIST =
 (SID_DESC =
 (SID_NAME = PLSExtProc)
 (ORACLE_HOME = E:\Oracle10gXEUniv\app\oracle\product\10.2.0\server)
 (PROGRAM = extproc)
 )
 (SID_DESC =
 (SID_NAME = CLRExtProc)
 (ORACLE_HOME = E:\Oracle10gXEUniv\app\oracle\product\10.2.0\server)
 (PROGRAM = extproc)
 )
 (SID_DESC =
 (SID_NAME = XE)
 (ORACLE_HOME = E:\Oracle10gXEUniv\app\oracle\product\10.2.0\server)
 )
 LISTENER =
 (DESCRIPTION_LIST =
 (DESCRIPTION =
 (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC_FOR_XE))
 (ADDRESS = (PROTOCOL = TCP)(HOST = 127.0.0.1)(PORT = 1521))
 )
 )
 
 DEFAULT_SERVICE_LISTENER = (XE)
 ```
 
 其中
 ```(SID_DESC =
 (SID_NAME = XE)
 (ORACLE_HOME = E:\Oracle10gXEUniv\app\oracle\product\10.2.0\server)
 )```
 就是我们新添加的部分。

 **注意该实例描述的ORACLE_HOME后面不能像其它实例那样加(PROGRAM = extproc),否则会报“ORA-28547: TNS: 连接服务器失败，可能是Net8管理错误。**
