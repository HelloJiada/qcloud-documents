## 操作场景
本文档指导您如何初始化 SDK。


## 操作步骤
1. 在 game.js 文件中，将启动页改为 MainView，
2. 完成 SDK 监听器初始化、实例化 Room 对象。玩家的 openId 使用 Util.js 中的 mockOpenId 方法生成。

game.js 最终代码如下所示：
```
// 导入 MGOBE.js
import "./MGOBE.js";
// 获取 Room、Listener 对象
const { Room, Listener, ErrCode, ENUM } = MGOBE;

import * as Util from "./Util.js";
const Global = Util.Global;

// 导入页面
import "./view/MainView.js";
import "./view/RoomView.js";
import "./view/GameView.js";

const gameInfo = {
  version: 'v1.0',
  // 替换 为控制台上的“游戏ID”
  gameId: 91000000,
  // 随机生成 玩家 ID
  openId: Util.mockOpenId(),
  wxAppid: 'wx43c6c5xxxxxxxxx',
  // 替换 为控制台上的“密钥”
  secretKey: 'kJm9RZWL7xxxxxxxxxxxxxxxxxxx',
};

const config = {
  // 替换 为控制台上的“域名”
  url: 'access.wxlagame.com',
  reconnectMaxTimes: 5,
  reconnectInterval: 1000,
  resendInterval: 1000,
  resendTimeout: 10000,
  autoRequestFrame: true,
};

// 初始化 Listener
Listener.init(gameInfo, config);

// 实例化 Room 对象
const room = new Room();

// 接收广播
Listener.add(room);

// 保存常用对象的引用
Global.room = room;
Global.ErrCode = ErrCode;
Global.ENUM = ENUM;
Global.gameInfo = gameInfo;

// 启动页为 MainView
new Global.MainView();
```
