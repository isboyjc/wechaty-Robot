# wechaty-Robot
基于wechaty-puppet-padplus的微信机器人助手



## 背景

我是一名前端，平时也喜欢写技术博客和交朋友，为此我也创建了微信技术交流群和微信公众号，一般我都会在文章下面贴出公众号和我的个人二维码，给有兴趣的小伙伴们添加微信然后我再拉他们进群这些，但是不停的同意微信好友验证，再发送群邀请真的是太痛苦了，相信很多做公众号的小伙伴都和我一样，作为一名开发，这种重复劳动是绝对不能忍受的

我知道也见过有些博主的微信小号是机器人，很方便，如果我也能有一个机器人小号，只是自动通过好友验证，然后关键字回复直接发送群邀请就已经非常实用了，嗯～，想想还有些兴奋

SO，大概在19年10月吧，就陆陆续续开始了我的微信机器人之旅

~~首先，我找了几个微信机器人平台，奈何价格实在不美丽~~ 

笑话，咱可是一名正八经的开发，这种非技术手段我会用？( 其实是没得钱噻！😅 )

说干就干，不过要从0到1的开发不太现实，所以就开始 Github 上寻找开源作品

对比了几个比较知名的几个开源微信机器人项目

- itchat
  - `itchat`是一个开源的微信个人号接口，基于python调用微信
  - 使用不到三十行的代码，你就可以完成一个能够处理所有信息的微信机器人
- wechaty
  - `Wechaty`是适用于微信个人的Bot SDK ，可以使用6行 js 创建一个机器人
  - 具有包括`linux`，`Windows`，`MacOS`和 `Docker` 在内的跨平台支持，基于Node.js
- Vbot
  - 是基于微信web版的接口，使用`http`协议以及轮询方式实现
  - `Vbot`的亮点在于通过匿名函数，能够实现多种有趣的玩法
  - 通过 API，更方便的打造属于自己的网页版微信，基于PHP

上面这些都是项目官方的简述，直接 `copy` 来的，刚看到这三款作品时，想都没想，果断选择`wechaty`

为什么？单论第一印象

- 对于一名前端来说，Node.js的亲和力自然不用多说
- `itchat`官方说不到三十行代码实现，`Vbot`就没说多少行，`Wechaty`抛开 JS ，官方说只用6行

没错，就是因此，我开始了 `wechaty` 的第一次亲密接触



## 第一次接触wechaty

Wechaty是基于`NodeJS+TS`实现

当然开发时我们不一定非要使用TS，js也可以的，这也是我个人很喜欢`Wechaty`团队的一点，因为官方给的示例都是基于 js 的而不是 ts，不习惯 ts 的小伙伴有福了

开发前，肯定是要先查看wechaty文档的，一看还别说，感觉还真挺容易上手的

- [wechaty-Github](https://github.com/wechaty/wechaty) 

简单的看了一下文档后，我开始下载官方给的示例项目 [wechaty/wechaty-getting-started](https://github.com/wechaty/wechaty-getting-started) 

下载完之后就是安装依赖运行

首次运行很慢的，还有可能不成功，因为中间要安装运行`Puppeteer`，有人可能要试好多次

然而这些我都没遇到，运行很成功，一切都很顺利，完全没有意外发生，哈哈哈

运行成功后如下图，就可以扫码登录了

![image-20200226180859522](../web-knowledge/else/简单实用的微信机器人小助手.assets/image-20200226180859522.png)



然后，意外就发生了😬



![image-20200226181313773](../web-knowledge/else/简单实用的微信机器人小助手.assets/image-20200226181313773.png)



登录不成功，真是尴尬

```js
"为了你的帐号安全，此微信号不能登录网页微信。你可以使用Windows微信或Mac微信在电脑端登录。Windows微信下载地址：https://pc.weixin.qq.com  Mac微信下载地址：https://mac.weixin.qq.com"
```



## 网页版微信登录不成功

当初其实卡在这里很久，我重复试了好多次都不行

原因是因为目前我们使用的是基于web端的微信API接口，可能是web端接口什么的都不太安全吧

微信官方在慢慢收缩web端微信的使用，官方对网页版微信进行了动态安全策略调整

如登录网页版微信收到安全提示，则不支持登录网页版微信

2017年之后注册的微信号都无法登录网页版微信，而2017年之前注册得微信账号也有很大几率登录不上

我赶紧试了试我的所有微信号，都是很早就注册的那种，可是依旧是登录不上，跑起来了登不上，这岂不是凉了

到了最后终于使用我一个朋友的微信号登上了，但是那是朋友的大号，人家要用的

后来我就到处找这个东西的解决办法，连带上花钱收可以登录网页版微信的号，拖了好些天依旧无果

检验你的微信号只不支持web端微信，尝试登录一下网页版微信就好了

- https://wx.qq.com/

就这个链接，PC端进入然后手机扫码登录，可以登上就是可用web微信

早期其实 `Vbot` 和 `itchat` 这两个项目都挺火的，但是它们都是基于网页版微信实现的

特别是`itchat` 项目的`Github issuse`中第一个就写着

![image-20200226191429357](../web-knowledge/else/简单实用的微信机器人小助手.assets/image-20200226191429357.png)



登录不上去的在这里劝大家一句，不要在这个问题上纠结太久

有渠道的小伙伴可以尝试收一个可以登录网页版微信的号，不过亲测很难

没有号的小伙伴就不要纠结了，没什么用又浪费时间，亲身经历(某人曾明知道官方限制，还依旧偏执的找解决方案找了好多天😭)

看到这里你可能会说：看了这么多了你跟我说不行？

不要着急，如果你使用`Vbot`和`itchat`，没有可登录的微信号确实是往下进行不了

但是我们现在使用的是`wechaty`，接下来就可以体现`wechaty`的过人之处了

当然如果你可以登录，那就可以看着官方文档或示例开发了，很省事

你也可以继续看看下文我写的一个小demo，虽然协议不同，不过API和思路都是一致的

如果你登录不上，那就更要看下解决办法了



## wechaty-puppet-padplus

网页版微信登录不上？收可登录微信号又收不到？

不要着急

`wechaty-puppet-padplus`同是`wechaty`团队开发，不同于上文基于微信web端，它是基于iPad协议

- [wechaty-puppet-padplus](https://github.com/wechaty/wechaty-puppet-padplus) 

使用这个包是需要 `Token` 令牌的，官方说

> Our Mission: Make it easy to build a WeChat Chatbot for developers.
>
> We provide a **free** access using [iPad protocol](https://github.com/wechaty/wechaty-puppet-padplus) for the developers who have a strong will and ability to build a valuable chatbot for users.
>
> Any developers can add JuziBOT Inc's staff ( **Wechat number : botorange_yeah** ) as a Wechat friend. You will receive a review form after adding. If you pass the review and willing to write a blog in Wechaty , you can use our iPad protocol for free！
>
> 
>
> 我们的使命：轻松为开发人员构建微信聊天机器人
>
> 我们为有强烈意愿和能力为用户构建有价值的聊天机器人的开发人员提供了使用[iPad协议](https://github.com/wechaty/wechaty-puppet-padplus)的**免费**访问权限
>
> 任何开发人员都可以将JuziBOT Inc的工作人员（**微信编号：botorange_yeah**）添加为微信好友。添加后，您将收到一份审查表。如果您通过审查并愿意在Wechaty中写博客，则可以免费使用我们的iPad协议！

大概意思就是我们提交审查表后，会获得为期15天的免费Token

想要获取长期有效的免费token，那就参加所谓的开源激励计划，就是在15天后，需要提交一个MVP(最小可行化产品)的Github仓库，Wechaty会将其fork到社区中的同时，会提供一个长期免费Token

反之，就需要继续协商讨论后续的合作形式，我觉得是很良心了

没错，这篇帖子就是我申请的15天免费token下的一个输出

当然，我是有时间就会写一些，毕竟时间不多，所以开发出来的东西功能也不多，后期慢慢改进吧

讲了这么多，接下来才是正经的分享，比较简单，算是入门级，供大家参考吧



## 基于ipad协议的微信机器人

### 明确需求

开发之前，我们要先明确下需求，就是我需要机器人来做什么

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

OK，先实现这几个简单的功能吧，还是比较有用的，后期再说后期的事嘛



### 项目结构

功能比较简单，分多个就是为了不让所有代码都在一个文件，简单分开下

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



### 初期准备

首先新建文件夹，初始化

```js
npm init -y
```

接着我们安装比较重要的核心包

```js
// Wechaty核心包
npm install --save wechaty

// padplus协议包
npm install --save wechaty-puppet-padplus
```

我们在开发过程中，还需要用到`qrcode-terminal`这个包，作用就是将二维码输出在终端来供我们扫码登录

```js
npm install --save qrcode-terminal
```

然后就可以愉快的开发了，没错就是这么简单



### 配置文件

所谓的配置文件，就是那个 `config.js` ，只是把我们需要用到的一些可配置参数拿出来

```js
module.exports = {
  // puppet_padplus Token
  token: "你自己申请的ipad协议token",
  // 你的机器人名字
  name: "圈子",
  // 房间/群聊
  room: {
    // 管理群组列表
    roomList: {
      // 群名字(用于发送群名字加群):群id，后面会介绍到
      Web圈: "*****@chatroom",
      男神群: "*****@chatroom"
    },
    // 加入房间回复
    roomJoinReply: `你好，欢迎加入`
  },
  // 私人
  personal: {
    // 好友验证自动通过关键字
    addFriendKeywords: ["加群", "前端"],
    // 是否开启加群
    addRoom: true
  }
}
```





### 入口文件

入口文件，也就是我们 `src` 目录下的 `index.js` 文件

这里做的很简单，没有逻辑

首先引入我们包

```js
const { Wechaty } = require("wechaty") // Wechaty核心包
const { PuppetPadplus } = require("wechaty-puppet-padplus") // padplus协议包
const config = require("./config") // 配置文件
```

接着初始化我们的bot

```js
// 初始化
const bot = new Wechaty({
  puppet: new PuppetPadplus({
    token: config.token
  }),
  name: config.name
})
```

接下来一段链式调用，监听，启动，完事

```js
const onScan = require("./onScan")
const onRoomJoin = require("./onRoomJoin")
const onMessage = require("./onMessage")
const onFriendShip = require("./onFriendShip")

bot
  .on("scan", onScan) // 机器人需要扫描二维码时监听
  .on("room-join", onRoomJoin) // 加入房间监听
  .on("message", onMessage(bot)) // 消息监听
  .on("friendship", onFriendShip) // 好友添加监听
  .start()
```

上面代码都有注释，`scan, room-join, message, friendship` 这些都是我们各个阶段的事件监听

- scan 机器人需要扫描二维码时监听
- room-join 加入房间监听
- message 消息监听
- friendship 好友添加监听

这些事件监听我只做简单解释，因为没啥说的，api文档都有

不由的想起尤大的那个表情包：请仔细阅读我们的文档！！！

这些个监听后面的回调，我这里只不过把他们单独拿出去了，也就是上文目录结构中的那几个文件

这里的`onMessage`是做了一个方法调用，其实还是返回一个回调函数，只不过我们在消息监听中用到了`bot`实例，所以用这种方式传值而已

接下来我们按顺序来解释下这几个文件做了什么



### onScan

`onScan` 文件是我们在机器人需要扫描二维码时的监听回调

这里面的代码超级简单

```js
const Qrterminal = require("qrcode-terminal")

module.exports = function onScan(qrcode, status) {
  Qrterminal.generate(qrcode, { small: true })
}
```

首先引入 `qrcode-terminal` 包

这个回调中其实做的很简单，回调接收了两个参数

- qrcode  qr码
- status  状态

我们借助`Qrterminal.generate`这个API将 qr 码输出到终端而已，后面那个`small`参数是因为`qrcode-terminal` 这个包默认输出的二维码太大了，给它变小一些



### onFriendShip

onFriendShip是friendship事件监听的回调，好友添加监听

```js
const { Friendship } = require("wechaty")
// 配置文件
const config = require("./config")
// 好友添加验证消息自动同意关键字数组
const addFriendKeywords = config.personal.addFriendKeywords

// 好友添加监听回调
module.exports = async function onFriendShip(friendship) {
  let logMsg
  try {
    logMsg = "添加好友" + friendship.contact().name()
    console.log(logMsg)
    switch (friendship.type()) {
      /**
       * 1. 新的好友请求
       * 设置请求后，我们可以从request.hello中获得验证消息,
       * 并通过`request.accept（）`接受此请求
       */
      case Friendship.Type.Receive:
        // 判断配置信息中是否存在该验证消息
        if (addFriendKeywords.some(v => v == friendship.hello())) {
          logMsg = `自动通过验证，因为验证消息是"${friendship.hello()}"`
          // 通过验证
          await friendship.accept()
        } else {
          logMsg = "不自动通过，因为验证消息是: " + friendship.hello()
        }
        break

      /**
       * 2. 友谊确认
       */
      case Friendship.Type.Confirm:
        logMsg = "friend ship confirmed with " + friendship.contact().name()
        break
    }
    console.log(logMsg)
  } catch (e) {
    logMsg = e.message
  }
}
```

如上所示，我们想加好友时，验证消息填写我们指定的文字可以自动通过

So，我们从配置文件中拿到这个参数，在新的好友请求过来时做一个判断即可



### onRoomJoin

onRoomJoin，也就是进入房间监听回调

```js
// 配置文件
const config = require("./config")
// 加入房间回复
const roomJoinReply = config.room.roomJoinReply
// 管理群组列表
const roomList = config.room.roomList

// 进入房间监听回调 room-群聊 inviteeList-受邀者名单 inviter-邀请者
module.exports = async function onRoomJoin(room, inviteeList, inviter) {
  // 判断配置项群组id数组中是否存在该群聊id
  if (Object.values(roomList).some(v => v == room.id)) {
    // let roomTopic = await room.topic()
    inviteeList.map(c => {
      // 发送消息并@
      room.say(roomJoinReply, c)
    })
  }
}
```

需求是在我们需要管理的群聊中，只要有新人加入，我们就发一个欢迎词并@他下

当然这些东西还是在config中配置好的，在这里拿到就可以

此回调接收三个参数

- room 群聊实例
- inviteeList 受邀者名单
- inviter 邀请者

有了房间，受邀者，邀请者，那么这里也就非常easy了

做一下判断就可以了，这里的`room.id`就是我们配置的管理群组列表对象的value值

为什么要有管理群组列表对象呢？因为我们在登录了一个微信号时，群组进入监听是针对微信号中所有群组的

我的需求是要管理我的群组，所以事先跑了下程序，输出了`room`，然后群里发个消息，就拿到了我想管理的群组所有信息，id自然也在里面，然后写到了配置里

接下来就是，监听到新加入，把受邀者列表遍历一下，使用`room.say`方法发送群消息即可，受邀者列表里存的就是加入的微信号实例，`say` 方法第一个参数就是要发送的消息，第二个参数就是为了@此人一下。。。感觉我的叙述毫无营养，还是那句话，这里只是说它是什么意思，具体API阅读文档吧，文档都有，也很简单





### message

最后就是message回调了，这个是代码最多的一个地方了，消息监听回调嘛

这也是代码中稍微有些逻辑的地方，因为要有各种判断

先不说程序逻辑，机器人嘛，总得能聊天不是，所以网上找了个免费的机器人聊天接口对接了一下

该接口详细请看

- https://drea.cc/mm.php

其实就是一个API，我们做一下封装，调用传入消息，返回消息，仅此而已

因为有请求，所以这块用了一个请求包，一个参数解码包，所以还要安装并引入下

```js
npm install --save request
npm install --save urlencode
```

把接口封装下，因为是免费机器人，所以肯定不是太好，不过个人用足够了，如下

```js
// node-request请求模块包
const request = require("request")
// 请求参数解码
const urlencode = require("urlencode")

/**
 * @description 机器人请求接口 处理函数
 * @param {String} info 发送文字
 * @return {Promise} 相应内容
 */
function requestRobot(info) {
  return new Promise((resolve, reject) => {
    let url = `https://open.drea.cc/bbsapi/chat/get?keyWord=${urlencode(info)}`
    request(url, (error, response, body) => {
      if (!error && response.statusCode == 200) {
        let res = JSON.parse(body)
        if (res.isSuccess) {
          let send = res.data.reply
          // 免费的接口，所以需要把机器人名字替换成为自己设置的机器人名字
          send = send.replace(/Smile/g, name)
          resolve(send)
        } else {
          if (res.code == 1010) {
            resolve("没事别老艾特我，我还以为爱情来了")
          } else {
            resolve("你在说什么，我听不懂")
          }
        }
      } else {
        resolve("你在说什么，我脑子有点短路诶！")
      }
    })
  })
}
```

接着就可以写消息监听回调的逻辑了，这里就不文字叙述了，太费劲了，注释很详细了，都是按行写的，哈哈

```js
const { Message } = require("wechaty")
// 配置文件
const config = require("./config")
// 机器人名字
const name = config.name
// 管理群组列表
const roomList = config.room.roomList

// 消息监听回调
module.exports = bot => {
  return async function onMessage(msg) {
    // 判断消息来自自己，直接return
    if (msg.self()) return

    // 判断此消息类型是否为文本
    if (msg.type() == Message.Type.Text) {
      // 判断消息类型来自群聊
      if (msg.room()) {
        // 获取群聊
        const room = await msg.room()

        // 收到消息，提到自己
        if (await msg.mentionSelf()) {
          // 获取提到自己的名字
          let self = await msg.to()
          self = "@" + self.name()
          // 获取消息内容，拿到整个消息文本，去掉 @+名字
          let sendText = msg.text().replace(self, "")
          // 请求机器人接口回复
          let res = await requestRobot(sendText)
          // 返回消息，并@来自人
          room.say(res, msg.from())
          return
        }

        // 收到消息，没有提到自己  忽略
      } else {
        // 回复信息是关键字 “加群”
        if (await isAddRoom(msg)) return
        // 回复信息是所管理的群聊名
        if (await isRoomName(bot, msg)) return
        // 请求机器人聊天接口
        let res = await requestRobot(msg.text())
        // 返回聊天接口内容
        await msg.say(res)
      }
    } else {
      console.log("消息不是文本！")
    }
  }
}

/**
 * @description 回复信息是关键字 “加群” 处理函数
 * @param {Object} msg 消息对象
 * @return {Promise} true-是 false-不是
 */
async function isAddRoom(msg) {
  // 关键字 加群 处理
  if (msg.text() == "加群") {
    let roomListName = Object.keys(roomList)
    let info = `${name}当前管理群聊有${roomListName.length}个，回复群聊名即可加入哦\n\n`
    roomListName.map(v => {
      info += "【" + v + "】" + "\n"
    })
    msg.say(info)
    return true
  }
  return false
}

/**
 * @description 回复信息是所管理的群聊名 处理函数
 * @param {Object} bot 实例对象
 * @param {Object} msg 消息对象
 * @return {Promise} true-是群聊 false-不是群聊
 */
async function isRoomName(bot, msg) {
  // 回复信息为管理的群聊名
  if (Object.keys(roomList).some(v => v == msg.text())) {
    // 通过群聊id获取到该群聊实例
    const room = await bot.Room.find({ id: roomList[msg.text()] })

    // 判断是否在房间中 在-提示并结束
    if (await room.has(msg.from())) {
      await msg.say("您已经在房间中了")
      return true
    }

    // 发送群邀请
    await room.add(msg.from())
    await msg.say("已发送群邀请")
    return true
  }
  return false
}
```



## 最后

就到这了，也希望对你能有些帮助，给点鼓励可以点个赞噻

看着文件和代码都不少，其实就只是一些逻辑判断而已

看一眼API文档，怎么发挥就看你自己了，消息监听这里的判断也只做了文本消息的判断而已

当然，你如果想用我这些东西，拉下代码`config.js`里换下token和一些配置信息就可以，当然我在不停更新，功能会越来越多，所以仓库中代码和文中会有些不一样，使用时简单看下代码，都写了详细注释，也很简单

- https://github.com/isboyjc/wechaty-Robot

目前实现的都是一些基础的小功能，登出和容错等一些处理也没有，因为这几天太忙了，后期慢慢加吧，这里就是为了给有想做但不知道的小伙伴简单介绍下wechaty，简单好用😄

还可以实现更多好玩的功能(我想到的功能只是针对我个人需求，只是为了和公众号、我的群聊等实现下无缝对接，你当然也可以做其他的嘛)，我现在能想到的后期要加的功能如下

- 推送
  - 例如每日早8点，拉取当日 `IT界新闻/掘金热门文章`发送至群聊
  - 群聊中可通过 `@[机器人]关键字` 查看新闻及文章等
  - 可设置定时任务，定时给自己/群聊发送消息
- 群聊功能消息管理
  - 监听群聊中消息，有不正当言论时或不文明用语对其警告
  - 记录同一人警告次数，每月清空记录，当月达到一定警告次数后自动将其移出群聊
- 群聊投票功能
  - 可通过机器人发起对某件事的群投票
- 群聊游戏
  - 猜字迷
  - 等等
- 后台管理系统(可视化配置及群聊数据统计)
  - 可视化配置机器人的已实现功能，包括登录等所有功能在web端可视化操作处理
  - 统计群聊中的成员活跃度/人员加入情况/警告等系列数据

来吧，生命在于折腾，好玩的东西总要试一试，毕竟费不了多少时间，你也可以加下我的小助手【圈子】微信体验下呦，验证消息写【前端】可以直接通过，和他聊聊天，或者加技术交流群我们一块玩耍都可以的

![WechatIMG127](../../../WechatIMG127.jpeg)

上线没几天，代码质量一般，服务器也不怎么样，所以bug会有的，如果你加小助手微信遇到了问题，也可以通过以下方式联系我或加群

![稿定设计导出-20200111-143924](../../公众号素材/公众号/稿定设计导出-20200111-143924.png)



