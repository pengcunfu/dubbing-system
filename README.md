# DubbingSystem 配音助手 基于SpringBoot+Vue开发的多人在线协作AI配音工具

* 调用魔音工坊开放平台API进行服务
* 调用讯飞、魔音、百度等语音合成API进行服务
* 调用百度语音识别API进行服务

目前只实现了魔音工坊API接口服务的调用。

## 项目目录结构

![1730648762908](D:\Data\Markdown\README\1730648762908.png)

推荐环境

* node 16.13.0
* npm 8.1.2
* mysql 8.0.12
* redis 3.0.504
* jdk 17

## 运行项目

```
npm run dev
```

```
npm run dev
```

## 部署项目

打包moyin-user

```
npm run build-only
```

打包moyin-admin

```
npm run build-admin
```

## 功能描述

* 配音功能
* 多人配音功能（暂未实现）
* 语音识别功能（暂未实现）

### SSML功能支持

* <speak>标签
* <break>标签
* <prosody>标签
* <say-as>标签
* <voice>标签
* <emphasis>标签
* <sub>标签
* <w>标签
* <p>标签
* <s>标签
* <phoneme>标签
* <audio>标签
* <mark>标签
* <phoneme>标签
* <say-as>标签
* <voice>标签
* <emphasis>标签
* <sub>标签
* <w>标签
* <p>标签

