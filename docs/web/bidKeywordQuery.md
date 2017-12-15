### 用户搜索关键字列表
>GET     `/bidKeywordQuery`

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
| `st.query`          | STRING | 用户搜索内容 |

**其他参数**

| 参数          | 说明              |
|:-------------|:-----------------|
| campaignId   | `必要` 广告系列ID  |
| adGroupId    | `必要` 广告组ID   |
| bidKeywordId | `必要` 关键字ID   |

```json
{
  "success": true,
  "data": {
    "total": 123,
    "rows": [
      {
        // 用户搜索内容
        "query": "iPhone",
        
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
      // ...
    ]
  }
}

```

