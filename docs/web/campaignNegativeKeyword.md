### 否定关键字列表
>GET     `/campaignNegativeKeywords`

**参数**

| 参数        | 说明                     |
|:-----------|:------------------------|
| campaignId | `必要` 广告系列ID         |
| state      | 状态: enabled, archived  |

**响应数据**
```json
{
  "success": true,
  "data": {
    "total": 123,
    "rows": [
      {
        // 广告系列否定关键字ID
        "campaignNegativeKeywordId": "0001",
        // 所属站点ID
        "profileId": "00011",
        // 所属广告系列ID
        "campaignId": "00111",
        // 状态 enabled, archived
        "state": "enabled",
        // 否定关键字内容
        "keywordText": "balala",
        // 匹配类型 negativeExact, negativePhrase
        "matchType": "negativeExact",
        // 创建时间
        "creationDate": 12312323000
      }
      // ...
    ]
  }
}
```

### 删除否定关键字
>DELETE  `/campaignNegativeKeywords/{campaignNegativeKeywordId}`

### 新建否定关键字
支持进度提示
>POST    `/campaignNegativeKeywords`

**参数**
```json
{
   // 所属系列ID
   "campaignId": "00111",
   // 否定关键字
   "negativeKeywords": [
      {
          // 否定关键字内容
          "keywordText": "balala",
          // 关键字匹配类型
          "matchType": "negativeExact"
      }
      //...
   ]
}
```

**响应**
```json
{
  "success": true,
  "data":[
    {
      // 否定关键字内容
      "keywordText": "balala",
      // 关键字匹配类型
      "matchType": "negativeExact",
      // 业务操作是否成功
      "success": true,
      // 失败消息
      "mesage": null
    }
    //...
  ]
}
```