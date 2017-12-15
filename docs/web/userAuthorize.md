
### 获取授权树
>GET     `/accounts/authorizes`

**参数**

| 字段     | 类型    | 说明          |
|:---------------------|:-------|:-------------|
| `accountIds`     | STRING | 账号id(多个逗号隔开：213,123,123)      |

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
			siteId: "US",
			campaigns: [{
				// 广告类型id
				campaignId: "00261",
				// 广告类型名称
				name: "ice cream maker-A"
			},
			{
				campaignId: "00325",
				name: "k cup coffee maker-A"
			}]
		}]
	}],
	errorCode: null
}

```

### 获取所有下级用户列表
>GET     `/accounts/subordinates`

**参数**

| 字段     | 类型    | 说明          |
|:---------------------|:-------|:-------------|
| `offset`     | NUMBER | 页码      |
| `litmit`     | NUMBER | 最大条数      |


**响应数据**

```json
{
	success: true,
	message: null,
	data: [{
		// 职称
		orgName: "xx人员",
		// 部门id
		groupId: 1070,
		// 职级
		orgLevel: 3,
		// userId
		userId: 490,
		// 部门类别名称
		categoryName: "xx类",
		// 职位id
		orgId: 10,
		// 组名
		groupName: "xxxx",
		// 仓库(无用字段)
		warehouse_no: 7,
		// 职位编码
		orgCode: "3003",
		// 用户账号
		account: "zhongkun@aukeys.com",
		// 用户邮箱
		email: "zhongkun@aukeys.com",
		// 部门类别id
		categoryId: 30,
		// 用户名
		username: "bb"
	}],
	errorCode: null
}

```

### 启用/禁用店铺
```text
PUT    /accounts/adjust
```

### 获取店铺列表
>GET     `/accounts`

**响应数据**

```json
{
	success: true,
	message: null,
	data: [{
		// 账户id
		accountId: "Firstfun",
		// 账户名
		accountName: "Firstfun",
		// 启用状态('enabled'启用,'disabled'禁用)
		state: "enabled",
		// 创建人
		creationUserId: 0,
		// 创建时间
		creationDate: "2017-07-29 15:26:44",
		// 最后更新时间
		lastUpdatedDate: "2017-07-29 15:26:47"
	}],
	errorCode: null
}

```

### 授权用户
>POST   /accounts/authorizes


**参数**
```json
userIds: [123,123],
accounts: [{
    // 账号id
	accountId: "Firstfun",
    // 账号名称
	accountName: "Firstfun",
	sites: [{
		// 站点id
		profileId: "00039",
		// 站点code
		siteId: "US",
		campaigns: [{
			// 广告类型id
			campaignId: "00261",
			// 广告类型名称
			name: "ice cream maker-A"
		},
		{
			campaignId: "00325",
			name: "k cup coffee maker-A"
		}]
	}]
}]
```
### 获取亚马逊账号
>GET     `/accounts/amazonAccounts`

**参数**


**响应数据**

```json
{
    	"success": true,
    	"message": null,
    	"data": {
    		"total": 164,
    		"rows": [{
    		        //账号ID
    				"accountId": "50",
    				//账号全称
    				"accountName": "amazonaukeys",
    				//状态
    				"state": null,
    				//创建人
    				"creationUserId": null,
    				//创建时间
    				"creationDate": null,
    				//更新时间
    				"lastUpdatedDate": null,
    			     //状态简称
    				"accountNameCode": "aukey.b2c.us"
    			}
    			//.....
    		]
    	},
    	"errorCode": null
    }
```
### 保存PPC账号
>POST     `/accounts/batchSave`

**参数**
```json
{
    ppcAccountList: [{
        //账号ID
        "accountId": "50",
        //账号全称
        "accountName": "amazonaukeys",
        //状态,默认启用
        "state": "enabled",
        //创建人
        "creationUserId": null,
        //创建时间
        "creationDate": null,
        //更新时间
        "lastUpdatedDate": null
       }
       //.....
	    ]
}
```

**响应数据**

  success
```