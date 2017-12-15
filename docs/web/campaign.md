### 广告系列列表数据
>GET     `/campaigns`

**参数(query)**

| 字段(alias.field)     | 类型    | 说明            |
|:---------------------|:-------|:---------------|
| `st.impressions`     | NUMBER | 展示次数        |
| `st.clicks`          | NUMBER | 点击次数        |
| `st.cost`            | NUMBER | 花费            |
| `st.ctr`             | NUMBER | 展示点击比      |
| `st.cpc`             | NUMBER | 每次点击花费     |
| `st.conversions`     | NUMBER | 订单数量        |
| `st.sales`           | NUMBER | 销售额          |
| `st.acos`            | NUMBER | ACOS           |
| `st.conversion_rate` | NUMBER | 订单转化率      |
| `cp.name`            | STRING | 广告系列名称     |
| `cp.state`           | STRING | 广告系列状态     |
| `cp.daily_budget`    | NUMBER | 广告系列预算     |
| `cp.start_date`      | DATE   | 广告系列开始时间 |
| `cp.end_date`        | DATE   | 广告系列截止时间 |

**其他参数**

| 字段      | 类型    | 说明                                                                |
|:---------|:-------|:-------------------------------------------------------------------|
| dateType | STRING | `必要` 日期类型, [dateType枚举](/web/main?id=列表查询参数dateType枚举) |
| listFrom | DATE   | 自定义日期起始时间                                                   |
| listThru | DATE   | 自定义日期截止时间                                                   |

**响应数据**
```json
{
  "success": true,
  "data": {
    "total": 123,
    "rows": [
        {
          // 广告系列ID
          "campaignId": "00001",
          // 站点ID
          "profileId": "0233",
          // 广告系列名称
          "name": "Campaign Name",
          // 触发类型, 手动/自动 manual/auto
          "targetingType": "manual",
          // 状态 启用/暂停/删除 enabled/paused/archived
          "state": "enabled",
          // 每日预算
          "dailyBudget": 123.33,
          // 开始时间
          "startDate": 1501748232000,
          // 截止时间
          "endDate": 1501748232000,
          
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
        //...
    ]
  }
}
```

### 创建广告系列
支持进度提示
>POST    `/campaigns`


**参数**
```json
{
  // 广告系列名称
  "name": "name",
  // 状态  enabled/paused/archived
  "state": "enabled",
  // 每日预算
  "dailyBudget": 123.22,
  // 起始时间
  "startDate": "yyyy-MM-dd",
  // 截止时间
  "endDate": "yyyy-MM-dd",
  // 触发类型  manual/auto
  "targetingType": "manual"
}
```

### 同步广告系列
支持进度提示
>POST    `/campaigns/sync`


**参数**
```
  // 列表类型名称
  "type": "campaign"(campaign, adGroup, keyword, productAd, negativeKeyword, campaignNegativeKeyword)
```

### 获取广告系列详细
>GET     `/campaigns/{campaignId}`



### 删除广告系列
>DELETE  `/campaigns/{campaignId}`

### 调整广告系列预算
>PUT     `/campaigns/adjust/dailyBudget`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  // 预算
  "dailyBudget": 44.4
}
```


### 调整广告系列开始时间和结束时间
>PUT     `/campaigns/adjust/startDateAndEndDate`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  // 起始时间
  "startDate": "yyyy-MM-dd",
  // 结束时间
  "endDate": "yyyy-MM-dd"
}
```

### 调整广告系列(全部字段)
>PUT    `/campaigns/adjust/all`

**参数**
```json
{
    // 广告系列ID
    "campaignId": "00001",
    // 起始时间
    "startDate": "yyyy-MM-dd",
    // 结束时间
    "endDate": "yyyy-MM-dd",
    // 状态
    "state": "enabled",
    // 每日预算
    "dailyBudget": 12.22
}
```

### 暂停/恢复广告系列
>PUT     `/campaigns/adjust/state`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  // 恢复/暂停  enabled/paused
  "state": "enabled"
}
```

### 导出广告系列
>POST     `/campaigns/export/basic`

导出参数与[广告系列列表数据](/web/campaign?id=广告系列列表数据)参数一致.


### 广告系列对比图表数据
>GET     `/campaigns/chart/fetchCompareData`



**参数**

| 字段(alias.field) | 类型     | 说明                                                                |
|:------------------|:---------|:--------------------------------------------------------------------|
| `firstField`      | STRING   | 第一个比较字段的名称                                                  |
| `secondFidle`     | STRING   | 第二个比较字段的名称                                                  |
| `startDate`       | DATE     | 开始日期                                                             |
| `endDate`         | DATE     | 结束日期                                                             |
| `isComWith`       | BOOLEAN  | 是否选择比较日期                                                      |
| `cwStartSate`     | DATE     | 比较开始日期，isComWith为true是才有值                                  |
| `cwEndSate`       | DATE     | 比较结束日期，isComWith为true是才有值                                  |
| `dateType`        | STRING   | 比较维度（dally--每日、weekly--每周、monthly--每月、quarterly--每季度） |


**响应数据**
```json
{
  "success": true,
  "data":{
    "firstFieldData":{
      //字段名称
      "field": "impressions", 
      //isComWith为false的时候的数据
      "dataBefore":[{
        //显示的日期
        "date":"2017-8-18",
        //对应的val
        "val":10
      }],
      //isComWith为true的时候的数据 
      "dataAfter":[{
        "date":"2017-8-18",
        "val":10
      }]
    },
    "secondFieldData":{
      "field":"clicks",
     "dataBefore":[{
        //显示的日期
        "date":"2017-8-18",
        //对应的val
        "val":10
      }],
      "dataAfter":[{
        "date":"2017-8-18",
        "val":10
      }]
    }
  }
}
```
### 广告系列页面基础数据(如: 下拉框)
>GET     `/campaigns/ui/basic`

**参数**

| 字段           | 说明                                                                    |
|:--------------|:-----------------------------------------------------------------------|
| state         | 广告系列状态, 默认全部, 可选值: `enabled` `paused` `archived`, 多个逗号隔开 |
| targetingType | 广告系列触发类型, 默认全部, 可选址: `manual`, `auto`                       |

**响应数据**
```json
{
  "success": true,
  "data": [
    {
      // 广告系列ID
      "campaignId": "00001",
      // 广告系列名称
      "name": "campaign Name",
      // 广告系列状态
      "state": "enabled",
      // 广告系列触发类型
      "targetingType": "auto"
    }
    //...
  ]
}
```