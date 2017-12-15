### 创建查询偏好
>POST    `/queryPreference`

**参数**
```json
{
  // 查询名称
  "preferenceName": "name1",
  // 查询所属页面(一般值为页面URL)
  "preferencePage": "page/aaa",
  // 查询所属页面下的Key, 用于一个页面存在多个查询区分使用
  "preferenceKey": "xxxListQuery",
  // 查询偏好的 查询表单JSON数据字符串
  "queryContentJson": "{...}"
}
```

### 更新查询偏好
>PUT    `/queryPreference`

**参数**
```json
{
  // ID
  "userPreferenceId": "00001",
  // 查询名称
  "preferenceName": "name1",
  // 查询所属页面(一般值为页面URL)
  "preferencePage": "page/aaa",
  // 查询所属页面下的Key, 用于一个页面存在多个查询区分使用
  "preferenceKey": "xxxListQuery",
  // 查询偏好的 查询表单JSON数据字符串
  "queryContentJson": "{...}"
}
```

### 删除用户偏好
>DELETE `/queryPreference/{userPreferenceId}`

### 获取用户查询偏好列表
>GET    `/queryPreference`

**参数**
```json
{
  // 查询所属页面(一般值为页面URL)
  "preferencePage": "page/aaa",
  // 查询所属页面下的Key, 用于一个页面存在多个查询区分使用
  "preferenceKey": "xxxListQuery"
}
```

**响应数据**
```json
{
  "success": true,
  "data": [
    {
      // ID
      "userPreferenceId": "00001",
      // 查询名称
      "preferenceName": "name1",
      // 查询所属页面(一般值为页面URL)
      "preferencePage": "page/aaa",
      // 查询所属页面下的Key, 用于一个页面存在多个查询区分使用
      "preferenceKey": "xxxListQuery",
      // 查询偏好的 查询表单JSON数据字符串
      "queryContentJson": "{...}"
    }
    //...
  ]
}
```

### 用户查询偏好JSON数据结构
```json
{
    "fields": [
        {
            "alias": "o",
            "field": "quantity",
            "operator": "GREATER_THAN",
            "type": "NUMBER",
            "value": ["123"]
        },{
            "alias": "o",
            "field": "name",
            "operator": "EQUAL_TO",
            "type": "STRING",
            "value": ["111"]
         }
        //...
    ],
    "sorts": [
        {
            "alias": "o",
            "field": "quantity",
            "sort": "ASC"
        },{
            "alias": "o",
            "field": "ctr",
            "sort": "DESC"
        }
    ]
}
```

### field字段说明

| 字段      | 类型    | 说明                           |
|:---------|:-------|:------------------------------|
| alias    | string | 后端查询语句数据库表别名         |
| field    | string | `必要` 后端查询语句数据库表字段名称  |
| operator | string | `必要` 运算符                   |
| type     | string | `必要` 数据字段数据类型           |
| value    | array  | `必要` 具体的查询值              |

### 运算符
| 值                       | 对应语句       | 说明         |
|:-------------------------|:--------------|:------------|
| EQUAL_TO                 | `=`           | 等于         |
| NOT_EQUAL_TO             | `<>`          | 不等于       |
| IS_NULL                  | `IS NULL`     | 为null      |
| IS_NOT_NULL              | `IS NOT NULL` | 不为null     |
| GREATER_THAN             | `>`           | 大于         |
| GREATER_THAN_OR_EQUAL_TO | `>=`          | 大于等于     |
| LESS_THAN                | `<`           | 小于         |
| LESS_THAN_OR_EQUAL_TO    | `<=`          | 小于等于     |
| IN                       | `IN`          | in          |
| NOT_IN                   | `NOT IN`      | not in      |
| LIKE                     | `LIKE`        | like        |
| NOT_LIKE                 | `NOT LIKE`    | not like    |
| BETWEEN                  | `BETWEEN`     | between     |
| NOT_BETWEEN              | `NOT BETWEEN` | not between |

### 数据类型

| 值       | 举例  | 说明              |
|:---------|:-----|:------------------|
| NUMBER   |      | 数字类型           |
| STRING   |      | 字符类型           |
| DATE     |      | 日期类型, 年月日   |
| DATETIME |      | 日期类型, 年月日时分秒  |


### sort字段说明

| 字段   | 类型    | 说明                              |
|:------|:-------|:---------------------------------|
| alias | string | 后端查询语句数据库表别名            |
| field | string | `必要` 后端查询语句数据库表字段名称  |
| sort  | string | `必要` 排序, 升序`ASC`, 降序`DESC` |

```text
DATE, DATETIME 类型分别对应的格式为:
DATE: yyyy-MM-dd
DATETIME: yyyy-MM-dd HH:mm:ss
```
