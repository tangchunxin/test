# WORK3.0.0(沧州版) 后台协议

## 注意事项
- 请求格式为 `url?randkey=&c_version=x.x.x&parameter={}`，`parameter` 中字段 `mod` 和 `platform` 的较为固定，
<font color=red>所以下面只提供 `parameter` 区别传入的参数</font>

``` json
request:
{
  randkey: ""
  , c_version: "3.0.2"
  , parameter:
  {
    mod: "Business"
    , act: "Xxx_xx"
    , platform: "gfplay"	// android: gfplay , ios: gfplay_ios
    ...
  }
}
```

- http 统一的返回格式为

``` json
response:
{
  code: 0 //是否成功 0 成功
  , desc: "XXXXX"	//描述
  , sub_code: 0	//出错类型 0 成功
  , sub_desc: ""	//sub_code 描述
  , data:{...}
}
```

reponse

参数名|类型|说明
---|:---:|---
`code` |`number`| 0 为成功
`desc` |`string/null`| 关于参数 code 的描述信息
`sub_code` |`number`| 0 为成功
`sub_desc` |`string`| 关于参数 sub_code 的描述信息
`data` |`json/null/not`| 请求返回的信息

**特别重要：** 

* <font color=red>`null` - 代表有字段没有赋值</font>
* <font color=red>`not` - 代表没有该字段</font>
* <font color=red>`*` - 参数名带星号, 客户端可以连字段都不写</font>
* <font color=red>注意同和参考的区别：“同”</font>

##### <font color=red>下面只提供 `parameter` 区别传入的参数；下面只提供 `data` 内的返回说明</font>

---


* [1 后台管理系统]()
`http://test.linfiy.com/mahjong/game_agent/city_agent/index.php`

* [2 权限系统]()
`http://test.linfiy.com/power_control/index.php`

* [3 用户系统]()
`http://test.linfiy.com/user_php70/index.php`

## 目录

* [1.1配置数据 get_conf](#get_conf)
* [1.2登录获取人员基本信息 agent_login_info](#agent_login_info)
* [1.3添加代理 add_agent](#add_agent)
* [1.4自己下级人员列表 agent_info_list](#agent_info_list)
* [1.5代理搜索 search_agent](#search_agent)
* [1.6玩家列表 play_list](#play_list)
* [1.7玩家充值记录 play_recharge_list_new](#play_recharge_list_new)
* [1.8把玩家踢出公会 bing_out_agent_id](#bing_out_agent_id)
* [1.9把玩家拉入黑名单 pull_blacklist](#pull_blacklist)
* [1.10黑名单列表 blacklist](#blacklist)
* [1.11代理收益统计 income_statistics](#income_statistics)
* [1.12更改代理 change_agent](#change_agent)
* [1.13读取kpi kpi_get](#kpi_get)
* [1.14 获得支付模块的订单号等信息 wx_get_out_trade_no](#wx_get_out_trade_no)
* [1.15 修改下级代理信息 chmod_agent_info](#chmod_agent_info)

* [2.1 直接删除人员信息 delete_agent_info](#delete_agent_info)
* [2.2 给玩家充值 play_recharge](#play_recharge)
* [2.3 给玩家充值的时候 无限制的 玩家搜索 play_find_by_id](#play_find_by_id)
* [2.4 下载全部代理购钻和消耗明细 all_agent_buy_list  暂无用](#all_agent_buy_list)
* [2.5 boss添加公司人员 boss_add_agent  ](#boss_add_agent)
* [2.6 公司人员直接给代理充值 ,有权限 boss_recharge_agent  暂无用](#boss_recharge_agent)
* [2.7 公司人员给代理或玩家扣钻 ,有权限 del_agent_amount  ](#del_agent_amount)
* [2.9 下载全部代理 all_agent](#all_agent)
* [2.10 查询玩家消耗情况  find_play_recharge](#find_play_recharge)
* [2.11 查询玩家录像播放码 find_play_video](#find_play_video)
* [2.12 更换上级代理及代理合并下级 chmod_p_aid](#chmod_p_aid)
* [2.13 分享添加代理 decrypt_add_agent](#decrypt_add_agent)
* [2.14 代理提现 extract_income](#extract_income)
* [2.15 代理提现列表 extract_income_list](#extract_income_list)
- [2.16 查看礼物兑换记录show_gift_exchange_log](#show_gift_exchange_log)
- [2.17 更改发货信息change_delivery_information](#change_delivery_information)
- [2.18 查看充值卡信息show_rechargeable_card](#show_rechargeable_card)
- [2.19 添加充值卡密码add_rechargeable_card](#add_rechargeable_card)
- [2.20 删除充值卡密码delete_rechargeable_card](#delete_rechargeable_card)
- [2.21 代理收益下载income_statistics_excel](#income_statistics_excel)
- [2.22 代理提现列表下载extract_income_list_excel](#extract_income_list_excel)
- [2.23 合伙人分成比例set_shared](#set_shared)
- [2.24 开通公会付费guild_pay](#guild_pay)
- [2.25 H5公众号支付 wx_get_jsapi](#wx_get_jsapi)



### RCP 接口
* [3.1 远程读取代理信息agent_info_game](#agent_info_game)



<h3 id="get_conf">1.1 配置数据 get_conf</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "get_conf"



<h3 id="agent_login_info">1.2 登录获取人员基本信息 agent_login_info</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "agent_login_info"
  `aid` | `number` | 账号id
  `key` | `string` | 登录用的key

  response.data

   参数名|类型|说明
  ---|:---:|---
  `encrypt_aid` | `string` | 加密id
  `time` | `number` | 加密时间
  `init_time` | `string` | 已提现范围开始
  `extract_date` | `string` | 已提现范围结束
  `extract_start_date` | `string` | 可提现范围开始
  `extract_end_date` | `string` | 可提现范围结束

  response.data.<font color=red>agent_info</font>

  参数名|类型|说明
  ---|:---:|---
  `aid` | `number` | 账号id
  `wx_id` | `string` | 微信号
  `name` | `string` | 姓名
  `provinces` | `string` | 省份
  `city` | `string` | 城市
  `p_aid` | `number` | 上级客户经理
  `type` | `number` | 身份(9总公司 ,8城市合伙人,1会长,2副会长)
  `opend_status` | `number` | 开通方式 1审核通过 2直接开通
  `status` | `number` | 状态 1审核中  2 审核通过  3审核不通过删除 4 查封中
  `audit_eid` | `number` | 操作人id
  `info` | `string` | 备注
  `last_amount` | `number` | 剩余钻数
  `close_down_info` | `string` | 查封备注
  `close_down_time` | `string` | 查封时间
  `init_time` | `string` | 初始化时间
  `month` | `string` | 月份
 


<h3 id="add_agent">1.3 添加客服经理 或客服（ 姓名 电话 手机验证码 ）add_agent</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "add_agent"
  `aid` | `number` | 账号id
  `key` | `string` | 登录用的key
  `num` | `number` | 公司添加城市合伙人 不需要短信验证码   (城市合伙人添加会长; 会长添加副会长需要这个字段)
  `children_aid` | `number` | 被开通客服(经理)手机号
  `name` | `string` | 姓名
  `wx_id` | `string` | 微信号
  `provinces` | `string` | 省份
  `city` | `string` | 城市



<h3 id="agent_info_list">1.4 自己下级人员列表 agent_info_list</h3>


  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "agent_info_list"
  `aid` | `number` | 账号id
  `key` | `string` | 登录用的key
  `page` | `number` | 页码 1
  `p_aid` | `number` | 查询下级人员的 aid


  response.data.<font color=red>agent_info</font>

  参数名|类型|说明
  ---|:---:|---
  `aid` | `number` | 账号id
  `wx_id` | `string` | 微信号
  `name` | `string` | 姓名
  `provinces` | `string` | 省份
  `city` | `string` | 城市
  `p_aid` | `number` | 上级客户经理
  `type` | `number` | 身份(9总公司 ,8城市合伙人,1会长,2副会长)
  `opend_status` | `number` | 开通方式 1审核通过 2直接开通
  `status` | `number` | 状态 1审核中  2 审核通过  3审核不通过删除 4 查封中
  `audit_eid` | `number` | 操作人id
  `info` | `string` | 备注
  `last_amount` | `number` | 剩余钻数
  `close_down_info` | `string` | 查封备注
  `close_down_time` | `string` | 查封时间
  `init_time` | `string` | 初始化时间
  `month` | `string` | 月份

 

<h3 id="search_agent">1.5 代理搜索 search_agent</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "search_agent"
  `aid` | `number` | 账号id
  `key` | `string` | 登录用的key
  `search_aid` | `number` | 被充值id号
  `type` | `number` | 表示可以全部代理,,,,(可以不传,表示只能查询下级代理)

  response.data.<font color=red>list</font>

  参数名|类型|说明
  ---|:---:|---
  `aid` | `number` | 账号id
  `wx_id` | `string` | 微信号
  `name` | `string` | 姓名
  `provinces` | `string` | 省份
  `city` | `string` | 城市
  `p_aid` | `number` | 上级客户经理
  `type` | `number` | 身份(9总公司 ,8城市合伙人,1会长,2副会长)
  `opend_status` | `number` | 开通方式 1审核通过 2直接开通
  `status` | `number` | 状态 1审核中  2 审核通过  3审核不通过删除 4 查封中
  `audit_eid` | `number` | 操作人id
  `info` | `string` | 备注
  `last_amount` | `number` | 剩余钻数
  `close_down_info` | `string` | 查封备注
  `close_down_time` | `string` | 查封时间
  `init_time` | `string` | 初始化时间
  `month` | `string` | 月份
  `p_num` | `number` | 总代id


<h3 id="play_list">1.6 玩家列表 play_list</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "play_list"
  `agent_id` | `number` | 被查询的代理 可为空
  `page` | `number` | 页码  1
  `play_id` | `number` | 玩家id  可为空
  `start_time` | `string` | 开始时间 可为空
  `end_time` | `string` | 结束时间 可为空

  response.data

  参数名|类型|说明
  ---|:---:|---
  `data_count` | `number` | 总数据数量
  `page_count` | `number` | 每页数量
  `list` | `array<json>` | 详细信息

  response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `uid` | `number` | 玩家id
  `currency` | `number` |当前剩余钻玩家id
  `room` | `number` | 当前所在房间号
  `is_room_owner` | `number` | 是否为房主
  `update_time` | `number` | 注册时间
  `last_game_time` | `string` | 最后修改时间
  `currency2` | `number` | 第二种货币剩余个数
  `agent_id` | `number` | 绑定的推广员
  `sum_money` | `number` | 共计充值金额
  `sum_currency` | `number` | 共计消耗钻石数量
  `status` | `number` | 状态  0正常  1黑名单中
  `name` | `string` | 玩家昵称
  `wx_pic` | `string` | 微信头像地址


<h3 id="play_recharge_list_new">1.7 玩家充值记录 play_recharge_list_new</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "play_recharge_list_new"
  `page` | `number` | 页码  1
  `keywords` | `number` | 搜索关键字,推广号id或者玩家id 有则传,没有则不传
  `start_time` | `string` | 开始时间 可为空
  `end_time` | `string` | 结束时间 可为空

  response.data

  参数名|类型|说明
  ---|:---:|---
  `data_count` | `number` | 总数据数量
  `page_count` | `number` | 每页数量
  `list` | `array<json>` | 详细信息

  response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `id` | `number` | 表的主键
  `uid` | `number` |玩家id
  `old_currency` | `number` | 充值之前的钻石
  `currency` | `number` | 钻石变化
  `type` | `number` | 支付方式  1 消费扣钻  2 代理充值   3 微信分享充值   4微信支付
  `time` | `string` | 最后修改时间
  `money` | `number` | 充值金额
  `name` | `number` | 玩家昵称


<h3 id="bing_out_agent_id">1.8 把玩家踢出公会 bing_out_agent_id</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "bing_out_agent_id"
  `aid` | `number` | 代理账号id
  `key` | `number` | 登录用的key
  `play_uid` | `string` | 玩家id
  `agent_id` | `string` | 工会id




<h3 id="pull_blacklist">1.9 把玩家拉入黑名单 pull_blacklist</h3>


 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "pull_blacklist"
  `aid` | `number` | 代理账号id
  `key` | `number` | 登录用的key
  `uid` | `string` | 玩家id
  `status` | `string` |  1 拉入黑名单 0 解除黑名单


<h3 id="blacklist">1.10 黑名单列表 blacklist</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "blacklist"
  `page` | `number` | 页码  1
  `keywords` | `number` | 搜索关键字,推广号id或者玩家id 有则传,没有则不传

  response.data

  参数名|类型|说明
  ---|:---:|---
  `data_count` | `number` | 总数据数量
  `page_count` | `number` | 每页数量
  `list` | `array<json>` | 详细信息

  response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `uid` | `number` | 玩家id
  `currency` | `number` |当前剩余钻玩家id
  `room` | `number` | 当前所在房间号
  `is_room_owner` | `number` | 是否为房主
  `update_time` | `number` | 注册时间
  `last_game_time` | `string` | 最后修改时间
  `currency2` | `number` | 第二种货币剩余个数
  `agent_id` | `number` | 绑定的推广员
  `sum_money` | `number` | 共计充值金额
  `sum_currency` | `number` | 共计消耗钻石数量
  `status` | `number` | 状态  0正常  1黑名单中
  `name` | `string` | 玩家昵称
  `wx_pic` | `string` | 微信头像地址


<h3 id="income_statistics">1.11 代理收益统计 income_statistics</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "income_statistics"
  `page` | `number` | 页码  1
  `p_aid` | `number` | 被点击人的agent_id 有则传,没有则不传
  `keywords` | `number` | 搜索关键字,推广号id或者玩家id 有则传,没有则不传
  `start_time` | `number` | 开始时间  有则传,没有则不传
  `end_time` | `number` | 结束时间  有则传,没有则不传

  response.data

  参数名|类型|说明
  ---|:---:|---
  `data_count` | `number` | 总数据数量
  `page_count` | `number` | 每页数量
  `total_recharge` | `number` | 总计充值金额
  `total_recharge_subordinate` | `number` | 下属充值
  `my_total_income` | `number` | 我的收益
  `my_percent` | `number` | 我的收益占比
  `list` | `array<json>` | 详细信息

  response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `aid` | `number` | 账号id
  `wx_id` | `string` | 微信号
  `name` | `string` | 姓名
  `provinces` | `string` | 省份
  `city` | `string` | 城市
  `p_aid` | `number` | 上级客户经理
  `type` | `number` | 身份(9总公司 ,8城市合伙人,1会长,2副会长)
  `opend_status` | `number` | 开通方式 1审核通过 2直接开通
  `status` | `number` | 状态 1审核中  2 审核通过  3审核不通过删除 4 查封中
  `audit_eid` | `number` | 操作人id
  `info` | `string` | 备注
  `last_amount` | `number` | 剩余钻数
  `close_down_info` | `string` | 查封备注
  `close_down_time` | `string` | 查封时间
  `init_time` | `string` | 初始化时间
  `update_time` | `string` | 初始化时间
  `month` | `string` | 月份
  `p_num` | `number` | 总代id
  `total_recharge` | `float` | 总充值
  `income_percent` | `float` | 分成占比
  `total_income` | `float` | 应得收益
  `subordinate_income` | `float` | 下属贡献
  `total_recharge_subordinate` | `float` | 下属充值


<h3 id="change_agent">1.12 更改代理 change_agent</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "change_agent"
  `aid_of_operator` | `number` | 操作人id
  `aid_before_change` | `number` | 更改前代理id
  `aid_after_change` | `number` | 更改后代理id
  `key` | `string` |   登录key
  `name` | `string` | 姓名
  `wx_id` | `string` | 微信id
  `num` | `number` | 验证码
  `provinces` | `string` | 省份
  `city` | `string` | 城市


<h3 id="kpi_get">1.13 读取kpi kpi_get</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "kpi_get"
  `aid` | `number` | 操作人id
  `key` | `string` |   登录key

  response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `id` | `number` | 表的主键
  `id_time` | `string` | 日期
  `all_user` | `number` | 总计用户
  `new_user` | `number` | 新用户
  `active_user` | `number` | 活跃用户
  `game_num` | `number` | 当天牌局
  `hour_user` | `array<json>` | 每小时活跃用户
  `recharge_direct` | `float` | 直属用户充值
  `recharge_subordinate` | `float` | 下属用户充值
  `play_time` | `number` | 每局时间
  `agent_id` | `number` | 工会id



<h3 id="wx_get_out_trade_no">1.14 获得支付模块的订单号等信息 wx_get_out_trade_no</h3>
 
 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "wx_get_out_trade_no"
  `aid` | `number` | 玩家id
  `amount` | `string` | 数量

 response.data

  参数名|类型|说明
  ---|:---:|---
  `appid` | `number` | appid
  `noncestr` | `string` | 随机字符串
  `package` | `number` | Sign=WXPay
  `partnerid` | `number` | 商户号
  `prepayid` | `number` | 预支付订单号
  `timestamp` | `number` | 时间戳
  `paysign` | `array<json>` | 签名


<h3 id="chmod_agent_info">1.15 修改下级代理信息 chmod_agent_info</h3>
 
 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "chmod_agent_info"
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `children_aid` | `number` | 下级代理id
  `name` | `string` | 名字  为空时候不做修改
  `wx_id` | `string` | 微信id    为空时候不做修改



<h3 id="delete_agent_info">2.1 直接删除人员信息 delete_agent_info</h3> 
 
 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "delete_agent_info"
  `shop` | `string` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `del_aid` | `number` | 被删除代理id
  `type` | `string` |1删除  2查封  3解封


<h3 id="play_recharge">2.2 给玩家充值 play_recharge</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "play_recharge"
  `shop` | `string` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `p_aid` | `number` | 玩家id
  `recharge_amount` | `number` |客服(经理)给  玩家充的钻数量
  `type` | `number` |充值类型 2 代理充值  23 后台红钻充值 35后台充值积分  43后台充值奖杯


<h3 id="play_find_by_id">2.3 特殊权限 给玩家充值的时候  无限制的  玩家搜索 play_find_by_id</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "play_find_by_id"
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `p_aid` | `number` | 玩家id

  
 response.data.<font color=red>play_user</font>

  参数名|类型|说明
  ---|:---:|---
  `userId` | `number` | 玩家id
  `nickName` | `string` | 玩家昵称
  `specialGold` | `number` | 剩余钻数
  `currency2` | `number` | 剩余红钻数
  `score` | `number` | 剩余积分
  `cup` | `number` | 剩余奖杯

<h3 id="all_agent_buy_list">2.4 特殊权限 下载全部代理购钻和消耗明细 all_agent_buy_list</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "all_agent_buy_list"
  `shop` | `string` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `time_end` | `number` | 今天时间

<h3 id="boss_add_agent">2.5 boss添加公司人员 boss_add_agent</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "boss_add_agent"
  `shop` | `string` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `children_aid` | `number` | 被添加的代理
  `name` | `string` | 名字
  `wx_id` | `string` | 微信号
  `type` | `number` | 添加公司身份9   添加合伙人8
  `provinces` | `string` | 省份
  `city` | `string` | 城市
  `shared` | `json` | {"9":0.3,"8":0.7,"1":0.5,"2":0.3}直属
  `sub_shared` | `json` | {"9":0.3,"8":0.7,"1":0.5,"2":0.3}下级


<h3 id="boss_recharge_agent">2.6 公司人员直接给代理充值 ,有权限 boss_recharge_agent</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "boss_recharge_agent"
  `shop` | `string` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `recharge_aid` | `number` | 被充值的代理
  `last_amount` | `string` | 充值钻数
  `type` | `number` | 1:支付宝 2:官方手动充值钻 3:代理返利 4:活动奖励 6:微信充值  9:代理扣钻
  `activity_info` | `string` | 官方充值 原因备注
 


<h3 id="del_agent_amount">2.7 公司人员给代理或玩家扣钻 ,有权限 del_agent_amount</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "del_agent_amount"
  `shop` | `string` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `recharge_aid` | `number` | 被充值的代理
  `last_amount` | `string` | 充值钻数
  `type` | `number` | 1玩家   2代理
  `activity_info` | `string` | 官方充值 原因备注
 

<h3 id="all_agent">2.9 下载所有代理  all_agent</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "all_agent"
  `shop` | `number` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key


<h3 id="find_play_recharge">2.10 查询玩家消耗情况  find_play_recharge</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "find_play_recharge"
  `shop` | `number` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `play_uid` | `number` | 玩家id
  `page` | `number` |页码

response.data

  参数名|类型|说明
  ---|:---:|---
  `data_count` | `number` | 总数据数量
  `page_count` | `number` | 每页数量
  `list` | `array<json>` | 详细信息

response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `id` | `number` | 主键id
  `uid` | `number` | 玩家id
  `old_currency` | `number` | 充值之前钻石数量
  `currency` | `number` | 充值数量
  `type` | `number` | 充值类型   1开房消费  2代理充值   3微信分享  4微信支付
  `time` | `string` | 充值时间
  `money` | `number` |充值金额



<h3 id="find_play_video">2.11 查询玩家录像播放码  find_play_video</h3>


 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "find_play_video"
  `shop` | `number` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `play_uid` | `number` | 玩家id
  `page` | `number` |页码

response.data

  参数名|类型|说明
  ---|:---:|---
  `data_count` | `number` | 总数据数量
  `page_count` | `number` | 每页数量
  `list` | `array<json>` | 详细信息

response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `id` | `number` | 播放码
  `rid` | `number` | 房间号
  `uid` | `number` | 房主uid
  `time` | `number` | 时间
  `game_type` | `number` | 游戏类别
  `play_time` | `number` | 本局时间


  <h3 id="chmod_p_aid">2.12 更换上级代理及代理合并下级 chmod_p_aid</h3>


 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "chmod_p_aid"
  `shop` | `number` | 权限字段
  `aid` | `number` | 玩家id
  `key` | `string` | 登录key
  `search_aid` | `number` | /查找要被替换的手机号
  `chmod_aid` | `number` |替换成新的手机号  
  `info` | `string` |备注信息   可为空  
  `type` | `number` |1:更换上级代理   2:  Ａ下级代理合并给Ｂ



<h3 id="decrypt_add_agent">2.13  分享添加代理 decrypt_add_agent</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "decrypt_add_agent"
  `aid` | `number` | 账号id
  `encrypt_aid` | `string` | 加密账号id
  `time` | `number` | 加密时间
  `num` | `number` | 公司添加城市合伙人 不需要短信验证码   (城市合伙人添加会长; 会长添加副会长需要这个字段)
  `children_aid` | `number` | 被开通客服(经理)手机号
  `name` | `string` | 姓名
  `wx_id` | `string` | 微信号
  `provinces` | `string` | 省份
  `city` | `string` | 城市

<h3 id="extract_income">2.14  代理提现 extract_income</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "extract_income"
  `aid` | `number` | 账号id
  `key` | `string` | 登陆key
  `start_time` | `number` | 收益开始时间 不能为空
  `end_time` | `number` | 收益结束时间 不能为空

<h3 id="extract_income_list">2.15 代理提现列表 extract_income_list</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "extract_income"
  `aid` | `number` | 账号id
  `key` | `string` | 登陆key
  `search_aid` | `number` | 被查询id 可为空
  `start_time` | `number` | 收益开始时间  不能为空
  `end_time` | `number` | 收益结束时间  不能为空

  response.data

  参数名|类型|说明
  ---|:---:|---
  `data_count` | `number` | 总数据数量
  `page_count` | `number` | 每页数量
  `list` | `array<json>` | 详细信息

response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `out_trade_no` | `number` | 订单号
  `uid` | `number` | 代理id
  `total_fee` | `number` | 提现jine
  `start_time` | `number` | 收益开始时间
  `end_time` | `number` |收益结束数据
  `status` | `number` |订单状态 状态 0 未提取 1 提取中  2 提取成功  4 提取失败 
  `notify_status` | `string` | 回调通知状态 0 未通知 1 通知成功 2通知失败
  `third_trade_no` | `number` |第三方微信订单号
  `third_party_type` | `number` |第三方支付平台类别： 1 支付宝 2 微信 3 银联 4微信提现
  `third_notify_info` | `number` |第三方回调 信息
  `init_time` | `number` | 创建时间
  `update_time` | `number` |支付成功时间

<h3 id="show_gift_exchange_log">2.16 查看礼物兑换记录</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "show_gift_exchange_log"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `shop` | `string` | 权限字段
  `state` | `number` | 兑换状态(1:待处理,2:处理中,3:已完成),当查全部时,此项不传
  `page` | `number` | 页码 1
  `uid` | `number` | 玩家id (可以不填,不填时查全部)

  response.data

  参数名|类型|说明
  ---|:---:|---
  `all_count` | `number` | 总项数
  `count_per_page` | `json` | 20 每页项目数

  response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `id` | `number` | id
  `name` | `string` | 礼物名称
  `picture` | `string` | 礼物图片
  `time` | `number` | 兑换时间
  `receiver_name` | `string` | 收件人姓名
  `receiver_cellphone` | `number` | 收件人手机号
  `receiver_address` | `string` | 收件地址
  `remark` | `string` | 备注(用于填写发货信息)
  `state` | `number` | 状态(1:待处理,2:处理中,3:已完成)

<h3 id="change_delivery_information">2.17 更改发货信息</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "change_delivery_information"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `shop` | `string` | 权限字段
  `gl_id` | `number` | 兑换记录id
  `remark` | `number` | 发货信息
  `state` | `number` | 要变更为哪种状态(可以选择变更为处理中或已完成)

<h3 id="show_rechargeable_card">2.18 查看充值卡信息</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "show_rechargeable_card"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `shop` | `string` | 权限字段
  `gid` | `number` | 充值卡类别
  `state` | `number` | 充值卡状态(1:可充值,2:不可充值),可以不填,不填时表示全部
  `page` | `number` | 页码 1

  response.data

  参数名|类型|说明
  ---|:---:|---
  `all_count` | `number` | 总项数
  `count_per_page` | `json` | 20 每页项目数

  response.data.<font color=red>list[0]</font>

  参数名|类型|说明
  ---|:---:|---
  `id` | `number` | id
  `password` | `string` | 充值卡密码
  `gid` | `number` | 充值卡种类
  `state` | `number` | 状态

<h3 id="add_rechargeable_card">2.19 添加充值卡密码</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "add_rechargeable_card"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `shop` | `string` | 权限字段
  `gid` | `number` | 充值卡类别
  `password` | `string` | 充值卡密码(如有多个密码,用逗号分隔)


<h3 id="delete_rechargeable_card">2.20 删除充值卡密码</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "delete_rechargeable_card"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `shop` | `string` | 权限字段
  `rc_id` | `number` | 充值卡密码ID



<h3 id="income_statistics_excel">2.21 代理收益下载</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "income_statistics_excel"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `shop` | `string` | 权限字段
  `start_time` | `string` | 开始时间
  `end_time` | `string` | 结束时间

<h3 id="extract_income_list_excel">2.22 代理提现列表下载</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "extract_income_list_excel"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `shop` | `string` | 权限字段
  `start_time` | `string` | 开始时间 可为空
  `end_time` | `string` | 结束时间 可为空
  `search_aid` | `number` | 搜索的id 可为空


<h3 id="set_shared">2.23 合伙人分成比例</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "set_shared"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `change_aid` | `number` | 被修改的代理
  `shop` | `string` | 权限字段
  `shared` | `string` | {"9":0.4,"8":0.6,"1":0.45,"2":0.3}直属
  `sub_shared` | `string` | {"9":0.4,"8":0.6,"1":0.45,"2":0.3}下属
  `third_shared` | `string` | {"9":0.4,"8":0.6,"1":0.45,"2":0.3}下下属
  `type` | `string` | 1修改change_aid比例  2修改全部比例


<h3 id="guild_pay">2.24  开通公会付费</h3>

  request.parameter

  参数名|类型|说明
  ---|:---:|---
  `act` | `string` | "guild_pay"
  `aid` | `number` | 登陆id
  `key` | `string` | 登陆key
  `encrypt_uid` | `string` | 灵飞码  当type=2,该字段可为空
  `type` | `string` | 1开通  2关闭

  <h3 id="wx_get_jsapi">2.25 H5公众号支付 wx_get_jsapi</h3>
 
 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "wx_get_out_trade_no"
  `aid` | `number` | 玩家id
  `amount` | `string` | 数量
  `openId` | `string` | 玩家openid
  `wx_type` | `string` | 商户平台模块 第一个传0  第二个传 1  以此类推

  response.data

  参数名|类型|说明
  ---|:---:|---
  `appId` | `number` | appid
  `nonceStr` | `string` | 随机字符串
  `package` | `number` | "prepay_id=wx201704251237197e335f1c440442820390"
  `signType` | `number` | 商户号
  `timeStamp` | `number` | 时间戳
  `paysign` | `array<json>` | 签名




### RCP 接口

  <h3 id="agent_info_game">3.1 远程读取代理信息 agent_info_game</h3>

 request.parameter

  参数名|类型|说明
  ---|:---:|---
  `mod` | `string` | "Business"
  `platform` | `string` | "gfplay"
  `act` | `string` | "agent_info_game"
  `aid` | `number` | 玩家id



