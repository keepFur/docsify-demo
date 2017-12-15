### 广告商品列表数据
>GET     `/productAds`

**参数(query)**

| 字段(alias.field)     | 类型    | 说明         |
|:---------------------|:-------|:------------|
| `st.impressions`     | NUMBER | 展示次数     |
| `st.clicks`          | NUMBER | 点击次数     |
| `st.cost`            | NUMBER | 花费         |
| `st.ctr`             | NUMBER | 展示点击比   |
| `st.cpc`             | NUMBER | 每次点击花费  |
| `st.conversions`     | NUMBER | 订单数量     |
| `st.sales`           | NUMBER | 销售额       |
| `st.acos`            | NUMBER | ACOS        |
| `st.conversion_rate` | NUMBER | 订单转化率   |
| `pa.sku`             | STRING | SKU         |
| `pa.asin`            | STRING | ASIN        |
| `pa.state`           | STRING | 广告商品状态  |


**其他参数**

| 参数        | 说明              |
|:-----------|:-----------------|
| campaignId | `必要` 广告系列ID  |
| adGroupId  | `必要` 广告组ID   |

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
          // 广告商品ID
          "productAdId": "0001",
          // SKU
          "sku": "ASDFDSF",
          // ASIN
          "asin": "SADFASDF",
          // 状态 启用/暂停/删除 enabled/paused/archived
          "state": "enabled",
          // SKU 图片地址
          "skuImgUrl": "http:/xxx.xxx.xxx/xxx.jpg",
          
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

### 创建广告商品
支持进度提示
>POST    `/productAds`

**参数**
```json
{
  // 广告系列ID
  "campaignId": "00001",
  // 广告组ID
  "adGroupId": "00001",
  "productAds": [
    {
      // 广告商品sku
      "sku": "0001",
      // 商品ASIN
      "asin": "23FSLKFJK"
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
      // 广告商品是否创建成功
      "success": true,
      // 创建失败附带错误消息
      "message": "",
      // 广告商品sku
      "sku": "0001"
    }
    //...
  ]
}
```

### 删除广告商品
>DELETE  `/productAds/{productAdId}`


### 暂停/恢复广告商品
>PUT     `/productAds/adjust`

**参数**
```json
[{
  // 广告系列ID
  "campaignId": "00001",
  // 广告组ID
  "adGroupId": "00001",
  // 广告商品ID
  "productAdId": "0001",
  // 暂停/恢复  paused/enabled
  "state": "paused"
}]
```

### 广告商品对比图表数据
>GET     `/productAds/chart/fetchCompareData`

### 导出广告商品
>GET     `/productAds/export/basic`