***NFD的
无欺诈/节点转发机器人

一个基于cloudflare worker的telegram 消息转发机器人，集成了反欺诈功能

***特点
基于cloudflare worker搭建，能够实现以下效果
搭建成本低，一个js文件即可完成搭建
不需要额外的域名，利用worker自带域名即可
基于worker kv实现永久数据储存
稳定，全球cdn转发
接入反欺诈系统，当聊天对象有诈骗历史时，自动发出提醒
支持屏蔽用户，避免被骚扰
***搭建方法
从@BotFather获取token，并且可以发送来禁止此Bot被添加到群组/setjoingroups
从uuidgenerator获取一个随机uuid作为秘密
从@username_to_id_bot获取你的用户ID
登录cloudflare，创建一个worker
配置worker的变量
增加一个变量，数值为从步骤1中获得的tokenENV_BOT_TOKEN
增加一个变量，数值为从步骤2中获得的secretENV_BOT_SECRET
增加一个变量，数值为从步骤3中获得的用户idENV_ADMIN_UID
绑定kv数据库，创建一个Namespace Name为的kv数据库，在setting -> variable中设置：nfd -> nfdnfdKV Namespace Bindings
点击，复制这个文件到编辑器中Quick Edit
通过打开来注册websokethttps://xxx.workers.dev/registerWebhook
***使用方法
当其他用户给bot发消息，会被转发到bot创建者
用户回复普通文字给转发的消息时，会回复到原消息发送者
用户回复, , 等命令会执行相关指令，不会回复到原消息发送者/block/unblock/checkblock
欺诈数据源
文件fraud.db为欺诈数据，格式为每行一个uid
可以通过pr扩展本数据，也可以通过提issue方式补充
提供额外欺诈信息时，需要提供一定的消息出处
