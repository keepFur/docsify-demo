### 操作进度展示
> 后端长时间操作, 前端实时进度展示, 为了简单前端使用了[HTML5 SSE](http://www.w3school.com.cn/html/html5_serversentevents.asp)

### 前端使用步骤
```javascript
//=== ① === 
var es = new EventSource('/servlet/h5_sse');

//=== ② === 
es.addEventListener('open', function(e) {
    if(e.data){
        //=== ③ === 
        var data = JSON.parse(e.data);
        $.ajax({
            url: "/dashboard/h5esTestControl",
            type: "get",
            data:{
                H5SSEID: data.id
            },
            success: function (data) {
            }
        });
    }
});

//=== ④ === 
es.addEventListener('message', function(e) {
    console.log(e.data);
});

//=== ⑤ === 
es.addEventListener('error', function(e) {
    console.log('=========error========');
    console.log(e.data);
    es.close();
    console.log('=========error========');
});

//=== ⑥ === 
es.addEventListener('close', function (e) {
    console.log('=========close========');
    console.log(e.data);
    es.close();
    console.log('=========close========');
});
```

- ① `var es = new EventSource('/servlet/h5_sse');` 构建EventSource对象URL为固定值 `/servlet/h5_sse`
- ② 监听`open`事件, 连接建立触发, 用于取得`H5SSEID`
- ③ 从Event对象中获取data并且取到`H5SSEID`, 发送具体长时间API Ajax调用并且在Header中提供`H5SSEID`参数
- ④ 监听`message`事件, 服务端推送消息触发, 主要进度处理与展示在这里
- ⑤ 监听`error`事件, 服务端推送异常消息触发
- ⑥ 监听`close`事件, 服务端推送关闭消息触发, 调用EventSource的close函数, 关闭连接.

### 事件data数据结构
```json
{
  // H5SSEID, 标识
  "id": 11,
  // errorCode
  "errorCode": null,
  // 进度描述内容
  "message": "",
  // 进度附带的数据对象, 视具体API而定
  "data": {
    // 进度最大值
    "maxValue":0,
    // 当前进度
    "nowValue":0,
    // 进度类型  success/warning/danger
    "progressType":"success"
   }
}
```

### 后端使用
```java
import com.aukey.st.amazon.ppc.core.h5sse.EventSourceCore;


//...
//...

//初始化EventSourceCore, 需要提供redisTemplate
EventSourceCore es = new EventSourceCore(redisTemplate);

int i = 0;
while (i <= 100) {
    i++;
    //推送消息
    es.pushMessage("处理数据中...", i);

    try {
        //模拟耗时操作
        Thread.sleep(5000);
    } catch (InterruptedException e) {
        e.printStackTrace();
        //发生异常, 推送ERROR 和 关闭事件
        es.pushErrorAndClose(e.getMessage(), null, null);
    }
}
//处理完成, 推送关闭事件
es.pushClose();

//...
//...

```