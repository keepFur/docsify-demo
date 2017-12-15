### 产品列表

_listing 服务的地址是 `http://amazon-listing.qa.aukeyit.com`_,允许跨域请求

> `GET` `/products`

> http://localhost:9016/products?sellerId=A1EPYTQDSE57XY&marketplaceId=ATVPDKIKX0DER

**参数** 分页参数默认为 offset, limit

| 字段             | 类型    | 说明                              |
|:----------------|:-------|:---------------------------------|
| `marketplaceId` | String |          |
| `sellerId`      | String |                                  |
| `asin`          | String | 这个及以下两个查询条件中，只能三选一  |
| `sellerSKU`     | String | sku                              |
| `productName`   | String | 产品名称                          |

**响应数据**
```json
{
  "success": true,
  "code": 200,
  "message": null,
  "data": {
    "total": 141,
    "rows": [
      {
        "id": 2,
        "itemName": "Aicok Stainless Steel Electronic Salt and Pepper Grinder Set with Adjustable Ceramic Coarseness LED lights (Pack of 2)",
        "listingId": "0606SWAAPGE",
        "productId": "B01JSA8QLM",
        "sellerSKU": "FF75137-FFTD",
        "price": 79.89,
        "openDate": 1496622278000,
        "quantity": null,
        "imageUrl": "http://ecx.images-amazon.com/images/I/518%2BlMU5A3L._SL75_.jpg",
        "asin": "B01JSA8QLM",
        "siteId": 24,
        "accountId": 469,
        "status": null
      }
    ]
  }
}
```

### 更新产品列表
> `GET` `/refresh`

**参数**

| 字段             | 类型    | 说明  |
|:----------------|:-------|:-----|
| `sellerId`      | String |      |
| `marketplaceId` | String |      |

**响应数据**
```json
{
  "success": true,
  "code": 200d
  "message": null,
  "data": null
}
```

**错误码**

| code  | 错误原因            |
|:------|:-------------------|
| `409` | 该账户站点正在更新中  |
