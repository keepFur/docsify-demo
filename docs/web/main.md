### 通用约定
Ajax请求的PUT, POST统一指定`Content-Type: application/json` <br/>

### 分页参数约定

`offset` 跳过指定条数

`limit` 每页大小

### Ajax响应数据结构
```json
{
    // 业务操作是否成功结果, true, false
    "success": true,
    // 业务操作消息
    "message": null,
    // 业务操作失败, 错误code
    "errorCode": null,
    // 服务器内部错误, 错误堆栈信息, 用于程序调试
    "exceptionStackTrace": null,
    // 操作响应数据对象
    "data": null
}
```

### 列表响应数据结构
```json
{
    "success": true,
    "message": null,
    "errorCode": null,
    "data": {
        // 数据总数
        "total": 1123,
        // 数据条目
        "rows": []
    }
}
```

### 通用查询数据结构
通用查询统一通过`query`参数进行递交数据,
比如通过通用查询获取广告系列 `http://localhost:8885/campaigns?query={query}` <br />
下面为query值的字符内容, 字段详细参考[用户查询偏好设置](/web/userQueryPreference)
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

**通用查询简单小栗子**

java
```java
    import com.aukey.st.amazon.ppc.external.mybatis.query.DynamicQueryHelper;

    //...
    @Autowired
    private PpcCampaignMapper ppcCampaignMapper;

    @RequestMapping(value = "/campaigns", method = RequestMethod.GET)
    public ResponseVO fetchCampaigns(HttpServletRequest request){
        //设置从request中动态获取条件
        DynamicQueryHelper.dynamicQueryWithRequest(request);
        //执行查询
        ppcCampaignMapper.testDynamicQuery("3330");
        
        return ResponseUtils.newResponse().succeed();
    }
    //...
```
Mapper Xml
```xml
<select id="testDynamicQuery" resultMap="BaseResultMap">
    SELECT * FROM
    ppc_campaign pc
    
    [dq_content]
        [dq_where]
            <!-- 这里填写自定义的where部分 -->
            pc.amazon_campaign_id is not null
            AND pc.campaign_id = #{campaignId}
        [/dq_where]
        
        [dq_group_by]
            <!-- 这里填写自定义的group by部分 -->
        [/dq_group_by]
        
        [dq_order_by]
            <!-- 这里填写自定义的order by部分 -->
            pc.creation_date desc
        [/dq_order_by]
    [/dq_content]
    
    LIMIT 1
</select>
```

### 日期类型数据格式

**响应**

响应日期类型返回时间戳(毫秒)

**提交**

提交服务端日期类型: DATE: `yyyy-MM-dd`, DATETIME: `yyyy-MM-dd HH:mm:ss`


### 列表查询参数dateType枚举

| 值             | 说明                   |
|:---------------|:----------------------|
| `BY_1DAY`      | 天, 用于自定义时间与昨天 |
| `THIS_WEEK`    | 本周（周一至今天）      |
| `THIS_WEEK_EX` | 本周（周日至今天）      |
| `LAST_7DAYS`   | 过去7天                |
| `LAST_WEEK`    | 上周（周一至周日）      |
| `LAST_WEEK_EX` | 上周（周日至周六）      |
| `LAST_14DAYS`  | 过去14天               |
| `THIS_MONTH`   | 本月                   |
| `LAST_30DAYS`  | 过去30天               |
| `LAST_MONTH`   | 上月                   |