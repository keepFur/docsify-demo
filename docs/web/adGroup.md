### 广告组列表数据
> GET     `/adGroups`

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
| `ag.name`            | STRING | 广告组名称    |
| `ag.state`           | STRING | 广告组状态    |
| `ag.default_bid`     | NUMBER | 广告组默认出价 |

**其他参数**

| 参数        | 类型    | 说明                                                                |
|:-----------|:-------|:-------------------------------------------------------------------|
| campaignId | STRING | `必要` 广告系列ID                                                    |
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
          // 广告组ID
          "adGroupId": "00001",
          // 广告系列ID
          "campaignId": "00001",
          // 站点ID
          "profileId": "0233",
          // 广告组名称
          "name": "adGroup Name",
          // 默认出价
          "defaultBid": 44.44,
          // 状态 启用/暂停/删除 enabled/paused/archived
          "state": "enabled",
          
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
          "conversionRate": 0.001,
          
          // amazon 建议出价
          "suggested": 111.11,
          // 市场最低出价
          "rangeStart": 11.1,
          // 市场最高出价
          "rangeEnd": 122.1
        }
        //...
    ]
  }
}
```

### 创建广告组
支持进度提示
>POST    `/adGroups`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  // 广告组名称
  "name": "adGroup Name",
  // 默认出价
  "defaultBid": 44.44,
  // 商品
  "productAds": [
    {
      "sku":"SKU_1"
    },{
      "sku": "SKU_2"
    }
  ],
  "bidKeywords": [
    {
      // 关键字文本
      "keywordText": "iPhone",
      // 匹配类型  exact/phrase/broad
      "matchType": "exact",
      // 关键字出价, 可选
      "bid": 111
    }
    //...
  ]
}
```

### 获取广告组列详细
>GET     `/adGroups/{adGroupId}`


### 删除广告组
>DELETE  `/adGroups/{adGroupId}`

**参数**

| 字段        | 说明              |
|:-----------|:-----------------|
| campaignId | `必要` 广告系列ID  |

### 调整广告组默认出价与状态(单个)
支持进度提示
>PUT `/adGroups/adjust/defaultBidAndState`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  // 广告组ID
  "adGroupId": "00002",
  // 默认出价
  "defaultBid": 22.22,
  // 状态 paused/enabled
  "state": "enabled"
}
```

### 调整广告组默认出价(批量)
支持进度提示
>PUT     `/adGroups/adjust/defaultBid`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  "adGroups": [
    {
      // 广告组ID
      "adGroupId": "00001",
      // 默认出价
      "defaultBid": 22.22
    }
    //...
  ]
}
```

**响应数据**
```json
{
  "success": true,
  "data":{
    "adGroups": [
      {
        // 被调整的广告组
        "adGroupId": "00001",
        // 调整的默认出价
        "defaultBid": 22.22,
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

### 暂停/恢复广告组
>PUT     `/adGroups/adjust/state`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  // 广告组ID
  "adGroupId": "00001",
  // 暂停/恢复  paused/enabled
  "state": "paused"
}
```

### 应用广告组建议出价(批量)
支持进度提示
>PUT     `/adGroups/adjust/applyRcmdBid`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  "adGroups": [
    {
      // 广告组ID
      "adGroupId": "00001",
      // 建议出价金额
      "rcmdBid": 33.33
    }
    // ...
  ]
}
```

**响应数据**
```json
{
  "success": true,
  "data":{
    "adGroups": [
      {
        // 广告组ID
        "adGroupId": "00001",
        // 建议出价金额
        "rcmdBid": 22.22,
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

### 广告组对比图表数据
>GET     `/adGroups/chart/fetchCompareData`


### 导出广告组
>POST     `/adGroups/export/basic`

导出参数与[广告组列表数据](/web/adGroup?id=广告组列表数据)参数一致.


### 广告组页面基础数据(如: 下拉框)
>GET     `/adGroups/ui/basic/`

**参数**

| 参数        | 说明                                                                   |
|:-----------|:----------------------------------------------------------------------|
| campaignId | `必要` 广告系列ID                                                       |
| state      | 广告组状态, 默认全部, 可选值: `enabled` `paused` `archived`, 多个逗号隔开  |

**响应数据**
```json
{
  "success": true,
  "data": [
    {
      // 广告组ID
      "adGroupId": "00001",
      // 广告组名称
      "name": "分组1",
      "state": "enabled"
    }
    //...
  ]
}
```