
# 共有api说明文档
## Hiwa公有api访问说明
- 私有api访问域名：https://oapi.hiwa.net.cn
- Hiwa公有api使用统一的数据返回结构：
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
## 公有api列表
### /open/partner/getAccessToken  获取访问凭据token
请求参数
```
{
	"key": "****",       //必填
	"secret": "****"     //必填
}
```
返回值：
```
{
	"ret": 0,
	"data": {
		"token": "8002....",
		"expire": 1542034887
	}
}
```
返回值说明:

|字段|详解|
|:---|:--|
|token|访问凭据token|
|expire|token失效时间戳, 根据该字段请自行缓存token|
