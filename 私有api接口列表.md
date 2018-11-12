
# 私有api说明文档
## 鉴权流程
Hiwa私有api是针对特定合作伙伴提供的数据接口，Hiwa将通过这些接口给合作伙伴提供私有或定制的数据，未经授权的用户无法调用。私有api调用流程如下：
1. 普通用户需要联系Hiwa客服（微信：**hiwa01**）或者发送邮件到 **majianping@hiwa-inc.com**，申请成为Hiwa合作伙伴。
2. Hiwa工作人员会在24小时内回复您的申请信息，符合Hiwa伙伴条件的用户将会收到Hiwa后台生成的伙伴账号（包括识别码key和密码secret）。
3. 合作伙伴使用识别码和密码请求token接口，获取访问凭据token。
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
	"token": "143c1a081903c06e4f499ff2c3376ee08",
	"coin": "btc"
}
```
返回值：
```
{
	"ret": 0,
	"data": {
		"name": "btc",
		"desc": "比特币（BitCoin）的概念最初由中本聪在2009年提出，根据中本聪的思路设计发布的开源软件以及建构其上的P2P网络。...",
		"image_url": "https://oss.hiwa.net.cn/icon/coin/btc.png",
		"ranking": 1,
		"supply_max": 21000000,
		"supply_total": 17372175,
		"supply_circulating": 17372175,
		"market_cap_percent": 52.42,
		"supply_total_percent": 52.42,
		"market_cap_usd": 111113871787
	}
}
```
字段说明：
```
字段|说明
--|:--|:
desc|币简介
desc|币简介
desc|币简介
desc|币简介
```
