
# 私有api说明文档
## 鉴权流程
Hiwa私有api是针对特定合作伙伴提供的数据接口，Hiwa将通过这些接口给合作伙伴提供私有或定制的数据，未经授权的用户无法调用。私有api调用流程如下：
1. 普通用户需要联系Hiwa客服（微信：**hiwa01**）或者发送邮件到 **majianping@hiwa-inc.com**，申请成为Hiwa合作伙伴。
2. Hiwa工作人员会在24小时内回复您的申请信息，符合Hiwa伙伴条件的用户将会收到Hiwa后台生成的伙伴账号（包括识别码key和密码secret）。
3. 合作伙伴使用识别码和密码请求token接口（[获取token](https://github.com/majianping110/Hiwa_Open_Api_Doc/blob/master/%E5%85%AC%E6%9C%89api%E6%8E%A5%E5%8F%A3%E5%88%97%E8%A1%A8.md#openpartnergetaccesstoken--%E8%8E%B7%E5%8F%96%E8%AE%BF%E9%97%AE%E5%87%AD%E6%8D%AEtoken)），获取访问凭据token。
4. 合作伙伴使用上一步获取的token，请求Hiwa私有api。
## Hiwa私有api访问说明
- 私有api访问域名：https://oapi.hiwa.net.cn
- 访问凭据token有效期为7200秒，请在token失效前重新获取token。
- 获取新token后，旧token会继续生效300秒，以方便业务平滑切换。
- Hiwa私有api使用统一的数据返回结构：
```
{
	"ret": 0, //成功返回0
	"data": 
}
```
或者
```
{
	"ret": -1, //失败返回-1
	"error": {
		"code": 500,
		"msg": "请求错误"
	}
}
```
## 私有api列表
###  /auth/coin/info    获取币的简介和市值信息
请求参数
```
{
	"token": "143c1a081903c06e4f499ff2c3376ee08",  //必填
	"coin": "btc"                                  //必填
}
```
返回值：
```
{
	"ret": 0,
	"data": {
		"name": "btc",
		"desc": "比特币（BitCoin）的概念最初由中本聪在2009年提出，根据中本聪的思路设计发布的开源软件以及建构其上的P2P网络...",
		"image_url": "https://oss.hiwa.net.cn/icon/coin/btc.png",
		"ranking": 1,
		"supply_max": 21000000,
		"supply_total": 17373450,
		"supply_circulating": 17373450,
		"market_cap_percent": 52.340000000000003,
		"supply_total_percent": 52.340000000000003,
		"market_cap_usd": 110251511912,
		"volume_24h_usd": 4321998947.4580898,
		"turnover_rate_24h": 3.9199999999999999
	}
}
```
返回值说明:

|字段|详解|
|:---|:--|
|name|币名称|
|desc|币简介|
|image_url|币图标|
|ranking|排名|
|supply_max|最大流通量（个）|
|supply_total|当前总流通量（个）|
|supply_circulating|当前交易流通量（个）|
|market_cap_percent|市值占比（百分比）|
|supply_total_percent|流通量占比（百分比）|
|market_cap_usd|市值（美元）|
|volume_24h_usd|24小时流通量（美元））|
|turnover_rate_24h|24小时换手率（百分比）|
###  /auth/panel/mood    获取大盘市场情绪
请求参数
```
{
	"token": "143c1a081903c06e4f499ff2c3376ee08",  //必填
}
```
返回值：
```
{
	"ret": 0,
	"data": {
		"activity_addresss": 250943,
		"trader_number": 127290,
		"activity_talk": 183621
	}
}
```
返回值说明:

|字段|详解|
|:---|:--|
|activity_addresss|活跃地址数|
|trader_number|活跃交易数|
|activity_talk|社群活跃数|
###  /auth/panel/market    获取大盘走势数据
请求参数
```
{
	"token": "143c1a081903c06e4f499ff2c3376ee08",  //必填
	"days":7
}
```
返回值：
```
{
	"ret": 0,
	"data": [{
		"time": 1542168120,
		"market_cap": 209498682303,
		"volume_usd": 13024414781.200001
	}, {
		"time": 1542082620,
		"market_cap": 212105007915,
		"volume_usd": 13282259141.200001
	}]
}
```
返回值说明:

|字段|详解|
|:---|:--|
|time|时间戳|
|market_cap|大盘流通量|
|volume_usd|大盘市值（美元）|
###  /auth/coin/ranking    获取币排行榜数据
请求参数
```
{
	"token": "143c1a081903c06e4f499ff2c3376ee08",  //必填
	"page_num":1,
	"page_size":50
}
```
返回值：
```
{
	"ret": 0,
	"data": [{
		"id": 52,
		"coin_name": "XRP",
		"coin": "XRP",
		"rank": 2,
		"circulating_supply": 40327341704,
		"total_supply": 99991780039,
		"max_supply": 100000000000,
		"usd_price": 0.3826129415,
		"last_updated": 1543409944,
		"turnover_rate": 4.38,
		"market_cap_percent": 11.44,
		"fiat_price": "¥3.3113",
		"market_cap": "¥1,072.71亿",
		"volume": "46.96亿",
		"rate": "6.9522",
		"change_percent": "9.92",
		"coin_img": "https:\/\/hiwa-inc.oss-cn-beijing.aliyuncs.com\/icon\/coin\/xrp.png"
	}]
}
```
返回值说明:

|字段|详解|
|:---|:--|
|time|时间戳|
|total_supply|当前总数量(个)|
|max_supply|最大数量（个）|
|turnover_rate|换手率（百分比）|
|market_cap_percent|市值占比|
|market_cap|总市值|
|volume|流通量|
|change_percent|涨跌幅|

