### PPC广告管理首页 (dashboard)


### 主界面
>GET     `/dashboard/control/index`


### 用户下账号站点列表 (数据权限)
>GET     `/dashboard/accountSites`

| 参数       | 说明           |
|:----------|:--------------|
| accountId | 站点ID, 模糊搜索 |

**响应数据**

```json
{
	success: true,
	message: null,
	data: {
		total: 1,
		rows: [{
        	// 账号id
			"accountId": "Firstfun",
        	// 账号名称
			"accountName": "Firstfun",
        	// 站点id
			"profileId": "00039",
        	// 站点code
			"site_id": "US"
		}]
	},
	errorCode: null
}
```

### 用户下账号站点列表 (数据权限)
>GET     `/dashboard/menuSites`

**响应数据**

```json
{
	success: true,
	message: null,
	data: [{
        // 账号id
		accountId: "Firstfun",
        // 账号名称
		accountName: "Firstfun",
		sites: [{
			// 站点id
			profileId: "00039",
			// 站点code
			siteId: "US"
		}]
	}],
	errorCode: null
}

```

### 切换账号站点
>POST    `/dashboard/useAccountSite`

**参数**
```json
{
    // 账号ID
    "accountId": "Firstfun",
    // 站点ID
    "profileId": "000292"
}
```
**响应**
```json
{
  	"success": true,
  	"message": null,
  	"data": {
  	    // 站点ID
        "profileId": "000292"
  	}
}
```



