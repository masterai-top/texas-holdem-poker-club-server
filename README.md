[简体中文](README.md) | [繁體中文](README.zh-TW.md) | [English](README.en.md) | [图文网站](https://masterai-top.github.io/texas-holdem-poker-club-server/)

# C++ 德州扑克俱乐部推送服务器源码

面向德州扑克俱乐部与多人房间的 C++/Tars 后端服务，重点处理消息推送、玩家在线状态、游戏状态、房间用户上报、广播通知和服务维护通知。仓库还提供产品界面截图，用于说明该服务在俱乐部、私人牌局和多玩法客户端中的集成场景。

> 本仓库公开部分主要是 `PushServer` 及相关协议，并非完整 Unity 客户端或全部游戏服务端。产品截图展示的是集成效果，具体模块、构建依赖与授权应以实际交付清单为准。

## 这个仓库解决什么问题

多人德州客户端不仅需要牌桌逻辑，还需要知道“谁在线、谁在哪个房间、何时推送消息、维护通知如何广播”。本项目把这些实时状态与通知职责集中在独立 PushServer：

1. 网关上报玩家在线状态与路由地址。
2. 服务查询单个或批量玩家的在线/游戏状态。
3. 房间上报玩家集合、桌子信息与在线统计。
4. PushServer 向指定玩家、多个玩家或全服广播消息。
5. 运维命令支持配置重载、在线状态清理、每日重置与维护通知。

## 可由源码核验的功能

| 模块 | 能力 | 代码依据 |
| --- | --- | --- |
| 消息推送 | 单用户、多用户消息与广播通知 | `PushServant.tars`、`PushServantImp.*` |
| 玩家状态 | 在线/离线、批量在线查询、在线玩家列表 | `UserStateProto.tars`、`UserStateProcessor.*` |
| 游戏状态 | 上报和查询玩家当前游戏状态 | `PushServant.tars`、`UserStateProcessor.*` |
| 房间上报 | 房间玩家、桌子信息与人数统计 | `reportRoomUsers`、`reportRoomTableInfo` |
| 运营通知 | 服务维护、红点、广播和玩家冻结通知 | `PushProto.tars`、`PushServantImp.h` |
| 数据访问 | MySQL 客户端与 DBAgent 代理 | `DBOperator.*`、`OuterFactoryImp.*` |

## 客户端玩法与流程展示

线上截图显示了快速加入/创建房间、创建俱乐部、现金桌、AOF、短牌、奥马哈、SNG、MTT、战绩、好友及多语言等入口。这些界面说明 PushServer 的应用场景，但不等同于本仓库单独包含全部对应玩法实现。

### 私人局流程

创建或加入牌局 → 配置盲注、买入、人数、Ante、时长及保险等选项 → 玩家进入房间 → 网关上报在线和游戏状态 → 服务推送房间消息及维护通知。

## 产品截图

| 创建牌局规则 | 玩法与人数设置 | 创建/加入俱乐部 |
| --- | --- | --- |
| <img src="docs/assets/images/screen-01.jpg" width="260" alt="德州扑克私人局规则设置"> | <img src="docs/assets/images/screen-03.jpg" width="260" alt="现金桌 AOF 短牌奥马哈设置"> | <img src="docs/assets/images/screen-04.jpg" width="260" alt="创建德州扑克俱乐部或牌局"> |

| 快速加入朋友局 | 俱乐部玩法大厅 | 战绩统计 |
| --- | --- | --- |
| <img src="docs/assets/images/screen-08.jpg" width="260" alt="输入房间号加入朋友局"> | <img src="docs/assets/images/screen-11.jpg" width="260" alt="德州扑克俱乐部多玩法大厅"> | <img src="docs/assets/images/screen-06.jpg" width="260" alt="德州扑克战绩统计"> |

## 技术结构

| 层级 | 仓库可确认内容 |
| --- | --- |
| 服务框架 | C++ 与 Tars Application/Servant |
| 服务接口 | `.tars` 协议，包含 Push、在线状态、游戏状态和广播结构 |
| 数据 | Tars MySQL 客户端、DBAgent 代理与配置读取 |
| 服务路由 | 按用户哈希选择代理并异步推送状态 |
| 运维 | reload、CleanOnlineUser、ServerUpdate、DailyReset 等管理命令 |
| 构建 | Linux Makefile；依赖外部 Tars 公共协议与内部模块 |

## 构建前提

`makefile` 引用了 `/home/tarsproto/XGame/DBAgentServer/DBAgentServer.mk` 及多项未随仓库提供的公共头文件和服务代理。仓库不能只靠一条 `make` 命令独立完成构建。请先准备匹配的 Tars、公共协议、DBAgent、配置文件和数据库环境，并删除或替换 Makefile 中硬编码的部署地址与凭据后再测试。

## 适合的搜索定位

本仓库重点覆盖：**德州扑克服务器源码、德州俱乐部推送服务、玩家在线状态、多人房间消息、C++ Tars poker server、poker push server、user presence service**。它与完整客户端仓库、赛事平台和牌桌 AI 项目形成明确区分。

## 联系与核验

Telegram：[@xuzongbin001](https://t.me/xuzongbin001) · Email：masterai918@gmail.com

使用前请核对源码范围、依赖、构建、知识产权及当地法规。本仓库不构成并发量、完整部署、收益或搜索排名承诺。

