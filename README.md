# wechaty-Robot

[![Powered by Wechaty](https://img.shields.io/badge/Powered%20By-Wechaty-green.svg)](https://github.com/chatie/wechaty)
[![Wechaty开源激励计划](https://img.shields.io/badge/Wechaty-开源激励计划-green.svg)](https://github.com/juzibot/Welcome/wiki/Everything-about-Wechaty)

基于 wechaty-puppet-padplus 的微信机器人助手



[Wechaty|NodeJS基于iPad协议手撸一个简单的微信机器人助手-掘金](https://juejin.im/post/5e5b2aeff265da5710438a1e)



#### 目前实现功能

- 自动通过好友验证
  - 当有人添加机器人时，判断验证消息关键字后通过或直接通过
  - 通过验证后自动回复并介绍机器人功能
- 私聊关键字回复
  - 例如回复 `加群` 推送群聊邀请
  - 例如回复 `作者微信` 推送作者微信名片
- 自动聊天
  - 群聊中通过 `@[机器人]xxx` 可以和机器人聊天
  - 私聊发送消息即可聊天
- 加入群聊自动欢迎
  - 当新的小伙伴加入群聊后自动 `@[新的小伙伴]` 发一个文字欢迎



#### 结构

```js
|-- src/
|---- index.js				# 入口文件
|---- config.js		  	# 配置文件
|---- onScan.js				# 机器人需要扫描二维码时监听回调
|---- onRoomJoin.js 	# 进入房间监听回调
|---- onMessage.js		# 消息监听回调
|---- onFriendShip.js	# 好友添加监听回调
|-- package.json
```



#### 最后

来吧，生命在于折腾，好玩的东西总要试一试，毕竟费不了多少时间，你也可以加下我的小助手【圈子】微信体验下呦，验证消息写【前端】可以直接通过，和他聊聊天，或者加技术交流群我们一块玩耍都可以的

![WechatIMG127](./README.assets/WechatIMG127.jpeg)

如果你加小助手微信遇到了问题，也可以通过以下方式联系我或加群

![20200111-143924](./README.assets/20200111-143924.png)
