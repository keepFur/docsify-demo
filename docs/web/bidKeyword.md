### 关键字列表数据
>GET     `/bidKeywords`

**参数(query)**

| 字段(alias.field)     | 类型    | 说明          |
|:---------------------|:-------|:-------------|
| `st.impressions`     | NUMBER | 展示次数      |
| `st.clicks`          | NUMBER | 点击次数      |
| `st.cost`            | NUMBER | 花费          |
| `st.ctr`             | NUMBER | 展示点击比    |
| `st.cpc`             | NUMBER | 每次点击花费   |
| `st.conversions`     | NUMBER | 订单数量      |
| `st.sales`           | NUMBER | 销售额        |
| `st.acos`            | NUMBER | ACOS         |
| `st.conversion_rate` | NUMBER | 订单转化率    |
| `kw.keyword_text`    | STRING | 关键字内容    |
| `kw.state`           | STRING | 关键字状态    |
| `kw.match_type`      | STRING | 关键字匹配类型 |
| `kw.bid`             | NUMBER | 关键字出价    |

**其他参数**

| 参数        | 类型    | 说明                                                                |
|:-----------|:-------|:-------------------------------------------------------------------|
| campaignId | STRING | `必要` 广告系列ID                                                    |
| adGroupId  | STRING | `必要` 广告组ID                                                     |
| dateType   | STRING | `必要` 日期类型, [dateType枚举](/web/main?id=列表查询参数dateType枚举) |
| listFrom   | DATE   | 自定义日期起始时间                                                   |
| listThru   | DATE   | 自定义日期截止时间                                                   |

**响应数据**

```json
{
  "success": true,
  "data": {
    "total": 123,
    "rows": [
      {
        // 竞价关键字ID
        "bidKeywordId": "00001",
        // 竞价关键字亚马逊ID
        "amazonKeywordId": "2342312323",
        // 所属站点ID
        "profileId": "00001",
        // 所属广告系列ID
        "campaignId": "0001",
        // 所属广告组ID
        "adGroupId": "0002",
        // 竞价关键字状态  enabled, paused, archived
        "state": "enabled",
        // 竞价关键字内容
        "keywordText": "iPhone",
        // 匹配类型 exact, phrase, broad
        "matchType": "exact",
        // 出价
        "bid": 12.2,
        // 建议出价
        "suggested": 11.11,
        // 市场最低出价
        "range_start": 9,
        // 市场最高出价
        "range_end": 15,
        
        // 展示次数
        "impressions": 123,
        // 成本(花费)
        "cost": 12.3,
        // 点击次数
        "clicks": 123,
        // 订单数量
        "conversions": 12,
        // 销售额
        "sales": 223.22,
        // ACOS (花费/销售额)
        "acos": 0.11,
        // 展示点击比 (展示次数/点击次数)
        "ctr": 0.002,
        // 每次点击花费 (花费/点击次数)
        "cpc": 11,
        // 订单转化率 (订单数量/点击次数)
        "conversionRate": 0.001
      }
    ]
  }
}

```


### 新建关键字
支持进度提示
>POST     `/bidKeywords`

**参数**
```json
{
    // 所属广告系列ID
    "campaignId": "0001",
    // 所属广告组ID
    "adGroupId": "0002",
    "keywords": [
      {
        // 关键字内容
        "keywordText": "iPad",
        // 匹配类型 exact, phrase, broad
        "matchType": "exact",
        // 出价
        "bid": 11.11
      }
      //...
    ]
}
```

**响应内容**
```json
{
  "success": true,
  "data": [
    {
      // 关键字内容
      "keywordText": "",
      // 匹配类型 exact, phrase, broad
      "matchType": "exact",
      // 出价
      "bid": 11.11,
      // 是否成功
      "success": false,
      // 错误信息
      "message": "关键字Keyword缺少[keywordText]参数"
    },{
      "keywordText": "iPhone",
      "matchType": "exact",
      "bid": 11.11,
      "success": true,
      "message": null
    }
    //...
  ]
}
```

### 删除关键字
>DELETE  `/bidKeywords/{bidKeywordId}`

**参数**
```json
{
  // 竞价关键字ID
  "bidKeywordId": "0001"
}
```

### 应用关键字建议出价(批量)
支持进度提示
>PUT `/bidKeywords/adjust/applyRcmdBid`

**参数**
```json
{
  // 所属广告系列ID
  "campaignId": "0001",
  // 所属广告组ID
  "adGroupId": "0002",
  // 关键字
  "keywords": [
    {
      // 关键字ID
      "keywordId": "001"
    }
    //...
  ]
}
```

**响应数据**
```json
{
  "success": true,
  "data": [
    {
      // 改关键字是否成功
      "success": true,
      // 失败错误信息
      "message": "",
      // 关键字ID
      "keywordId": "001"
    }
    //...
  ]
}
```

### 调整关键字出价(批量)
>PUT     `/bidKeywords/adjust/bid`

**参数**
```json
[{
  // 所属广告系列ID
  "campaignId": "0001",
  // 所属广告组ID
  "adGroupId": "0002",
  // 亚马逊keywordID
  "amazonKeywordId": "aa0001",
  // 关键字ID
  "bidKeywordId": "00001",
  // 出价
  "bid": 11.11
}]
```

**响应数据**
```json
{
  "success": true,
  "data":{
    "bidKeywords": [
      {
        // 被调整的关键字ID
        "bidKeywordId": "00001",
        // 调整的出价
        "bid": 11.11,
        // 业务是否执行成功
        "success": true,
        // 业务执行失败消息
        "message": "授权失败, 错误信息...."
      }
      // ...
    ]
  }
}
```

### 暂停/恢复关键字
>PUT     `/bidKeywords/adjust/state`

**参数**
```json
[{
  // 所属广告系列ID
  "campaignId": "0001",
  // 所属广告组ID
  "adGroupId": "0002",
  // 关键字ID
  "bidKeywordId": "00001",
  // 亚马逊keywordID
  "amazonKeywordId": "aa0001",
  // 状态 enabled, paused (恢复, 暂停)
  "state": "paused"
}]
```


### 关键字对比图表数据
>GET     `/bidKeywords/chart/fetchCompareData`

### 迁移关键字
支持进度提示
>POST    `/bidKeywords/operation/copy`

**参数**
```json
{
  // 所属广告系列ID
  "campaignId": "0001",
  "adGroup": {
    // 是否为新增 AdGroup
    "needCreate": true,
    // AdGroup name , needCreate 为 true, 必填
    "name": "Group 1",
    // AdGroup id, needCreate 为 false, 必填 
    "adGroupId": "0001"
  },
  // 关键字
  "keywords": [
    {
       // 关键字内容
      "keywordText": "iPad",
      // 匹配类型 exact, phrase, broad
      "matchType": "exact"
    }
    //...
  ]
}
```

### 导出关键字
>GET     `/bidKeywords/export/basic`
