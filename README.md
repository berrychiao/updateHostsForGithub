废弃
# GitHubHostsFlush

#### 解决在某些地区由于dns污染导致的GitHub网页打开缓慢的问题

**WebPageFetcher.java**文件是java脚本  需配合java jdk环境使用。

**若没有java编译器**，可编辑一个.bat文件。文件内容如下：

```更新githubHosts.bat

@ECHO OFF
setlocal EnableDelayedExpansion
color 3e
title 添加服务配置
 
PUSHD %~DP0 & cd /d "%~dp0"
%1 %2
mshta vbscript:createobject("shell.application").shellexecute("%~s0","goto :runas","","runas",1)(window.close)&goto :eof
:runas
set JDK_PATH=D:\jdk17\bin
%JDK_PATH%\javac -encoding utf8 WebPageFetcher.java   
%JDK_PATH%\java WebPageFetcher

ipconfig /flushdns
timeout /t 3600
```





**若JAVA配置了环境全局变量**，那么可删除 **set JDK_PATH=D:\jdk17\bin**及 **%JDK_PATH%\ **。
