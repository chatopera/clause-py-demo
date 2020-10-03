[![Docker Layers](https://images.microbadger.com/badges/image/chatopera/clause:develop.svg)](https://microbadger.com/images/chatopera/clause:develop "Image layers") [![Docker Version](https://images.microbadger.com/badges/version/chatopera/clause:develop.svg)](https://microbadger.com/images/chatopera/clause:develop "Image version") [![Docker Pulls](https://img.shields.io/docker/pulls/chatopera/clause.svg)](https://hub.docker.com/r/chatopera/clause/) [![Docker Stars](https://img.shields.io/docker/stars/chatopera/clause.svg)](https://hub.docker.com/r/chatopera/clause/) [![Docker Commit](https://images.microbadger.com/badges/commit/chatopera/clause:develop.svg)](https://microbadger.com/images/chatopera/clause:develop "Image CommitID")

# Clause Quick Start Guide / Clause 快速开始

Chatopera Language Understanding Service，Chatopera 语义理解服务

快速开始

![Sep-30-2019 23-14-13-min](https://user-images.githubusercontent.com/3538629/65892122-54ffc480-e3d8-11e9-8f64-c82f25694df5.gif)

## 前提

- 已部署 Clause 服务，参考[部署文档](https://github.com/chatopera/clause/wiki/%E6%9C%8D%E5%8A%A1%E9%83%A8%E7%BD%B2)

## 下载镜像

下载示例代码

```
git clone https://github.com/chatopera/clause-quick-start.git
cd clause-quick-start
```

## 安装依赖

安装 Clause Python Package

```
cd clause-quick-start
pip install clause
```

## 执行示例程序

```
cd clause-quick-start       # demo目录
CL_HOST=127.0.0.1           # 设置 Clause 服务的 IP 地址
CL_PORT=8056                # 设置 Clause 服务的端口
python bot.py               # 执行demo脚本
```

该脚本执行的示例代码[bot.py](https://github.com/chatopera/clause-quick-start/blob/master/bot.py)内有注释介绍如何完成：

| 步骤 | 说明                   |
| ---- | ---------------------- |
| 1    | 清除该机器人之前的数据 |
| 2    | 创建自定义词典         |
| 3    | 添加自定义词条         |
| 4    | 创建意图               |
| 5    | 添加意图槽位           |
| 6    | 添加意图说法           |
| 7    | 训练机器人             |
| 8    | 创建会话               |
| 9    | 和机器人对话           |

示例程序是一个点餐程序，输出内容如下：

```
[connect] clause host 127.0.0.1, port 8056
[clean_up_bot] remove intent take_out
[clean_up_bot] remove customdict food
[create] dict name food
[create] intent name take_out
[create] intent slot time
[create] intent slot loc
[create] intent slot food
[create] intent utter 我想订一份{food}
[create] intent utter 我想点外卖
[create] intent utter 我想点一份外卖，{time}用餐
[create] intent utter 我想点一份{food}，送到{loc}
[train] start to train bot ...
[train] in progress ...
[chat] human: 我想点外卖，来一份汉堡包
[chat] bot: 您想什么时候送到？
[chat] human: 今天下午5点
[chat] bot: 您希望该订单送到哪里？
[chat] human: 送到大望路5号20楼
[chat] bot: 好的
[session] 订单信息： 收集信息已完毕 True
    intent: take_out
    entities:
        food: 汉堡包
        time: 今天下午5点
        loc: 大望路5号
```

详细了解程序，[参考文档](https://github.com/chatopera/clause/wiki/%E7%A4%BA%E4%BE%8B%E7%A8%8B%E5%BA%8F)。

## 输入文件

需要强调的是，该示例程序使用了 [profile.json](https://github.com/chatopera/clause-quick-start/blob/master/profile.json) 文件作为机器人的输入数据，该文件描述了机器人的词典、说法和槽位等信息。

[profile.json](https://github.com/chatopera/clause-quick-start/blob/master/profile.json) 内容如下：

```
{
  "chatbotID": "bot007",
  "dicts": [
    {
      "name": "food",
      "dictwords": [
        {
          "word": "汉堡",
          "synonyms": "汉堡包;漢堡;漢堡包"
        }
      ]
    }
  ],
  "intents": [
    {
      "name": "take_out",
      "description": "下外卖订单",
      "slots": [
        {
          "name": "time",
          "dictname": "@TIME",
          "requires": true,
          "question": "您想什么时候送到？"
        },
        {
          "name": "loc",
          "dictname": "@LOC",
          "requires": true,
          "question": "您希望该订单送到哪里？"
        },
        {
          "name": "food",
          "dictname": "food",
          "requires": true,
          "question": "您需要什么食物?"
        }
      ],
      "utters": [
        {
          "utterance": "我想订一份{food}"
        }
      ]
    }
  ]
}
```

开发者可以很方便的通过修改这个文件复用[bot.py](https://github.com/chatopera/clause-quick-start/blob/master/bot.py)脚本训练和请求机器人对话服务。

## 停止服务并清空数据

恢复该示例项目到初始状态。

```
cd clause-quick-start
docker-compose down
docker-compose rm

sudo rm -rf ./var/mysql/data/*
sudo rm -rf ./var/activemq/data/*
sudo rm -rf ./var/redis/data/*
sudo rm -rf ./var/local/workarea/*
```

## 获得技术支持

创建新的 Issue
https://github.com/chatopera/clause/issues

<p align="center">
  <b>Clause QQ 交流群：809987971， <a href="https://jq.qq.com/?_wv=1027&k=5JpEvBZ" target="_blank">点击链接加入群聊</a></b><br>
  <img src="https://user-images.githubusercontent.com/3538629/64315364-6a095380-cfe4-11e9-8bf6-f15ce6e26e0a.png" width="200">
</p>

## 了解更多

Clause Wiki
https://github.com/chatopera/clause/wiki

- [概述](https://github.com/chatopera/clause/wiki/%E6%A6%82%E8%BF%B0)
- [系统设计与实现](https://github.com/chatopera/clause/wiki/%E7%B3%BB%E7%BB%9F%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%AE%9E%E7%8E%B0)
- [服务部署](https://github.com/chatopera/clause/wiki/%E6%9C%8D%E5%8A%A1%E9%83%A8%E7%BD%B2)
- [示例程序](https://github.com/chatopera/clause/wiki/%E7%A4%BA%E4%BE%8B%E7%A8%8B%E5%BA%8F)
- [开发环境搭建](https://github.com/chatopera/clause/wiki/%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA)
- [系统集成](https://github.com/chatopera/clause/wiki/%E7%B3%BB%E7%BB%9F%E9%9B%86%E6%88%90)
- [API 文档](https://chatopera.github.io/clause)
- [FAQ](https://github.com/chatopera/clause/wiki/FAQ)

<p align="center">
  <a href="https://github.com/chatopera/clause" target="_blank">
      <img src="https://user-images.githubusercontent.com/3538629/64316956-e4d46d80-cfe8-11e9-8342-ec8a250074bf.png" width="800">
  </a>
</p>

## 开源许可协议

Copyright (2019-2020) <a href="https://www.chatopera.com/" target="_blank">北京华夏春松科技有限公司</a>

[Apache License Version 2.0](https://github.com/chatopera/clause-quick-start/blob/master/LICENSE)

[![chatoper banner][co-banner-image]][co-url]

[co-banner-image]: https://user-images.githubusercontent.com/3538629/42383104-da925942-8168-11e8-8195-868d5fcec170.png
[co-url]: https://www.chatopera.com
