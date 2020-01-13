#  提交扫描件查询征信报告2.0任务银行卡版

## 调用说明

#### 请求参数


国银所有接口的请求参数都包含两个必要的基础属性：

|属性名|类型|是否必要|说明|
|--|--|--|--|
|token|String|是|国银分配给业务线的账号|
|creditOrderId|String|是|请求进件号，唯一的字符串|

#### 返回值
国银所有接口的返回数据包含了五个属性：

|属性名|类型|说明|
|--|--|--|
|serialNo|String|国银流水号，用来标识此次调用，该值唯一|
|code|String|返回码，用来标识此次调用的结果|
|message|String|返回结果描述，用来对返回结果码进行解释说明|
|success|boolean|返回调用成功状态，表示第三方是否返回了足以进行下一步业务处理的内容，与具体业务无关|
|t|Object|业务数据，在调用成功且查得的情况下该值非空|

**重要说明：调用获得返回值后，首先需要根据对象的success属性来判断此次调用是否成功（注意：推荐通过判断success的方式，不推荐对比结果返回码的方式)。如果为true，通过t属性的内容获取业务数据进行后续的业务处理。如果为false，则当做调用失败处理，以code和message分析失败原因。业务处理流程应依照业务数据的内容进行判断。**


## 接口说明
### 信扫描件查询报告提交任务
#### 调用https接口接入
生产地址：  
https://credit.szguoyinshengda.com/credit/zixin/submitScanningTaskV2WithAccount  
测试地址：  
https://credit-test.szguoyinshengda.com/credit/zixin/submitScanningTaskV2WithAccount  
请求方式：POST  
请求参数格式：json字符串  
返回格式及编码：application/json; charset=utf-8

#### 参数说明

|属性名|类型|是否必要|说明|
|--|--|--|--|
|token|String|是|国银分配给业务线的账号|
|creditOrderId|String|是|请求进件号，唯一的字符串|
|messageId|String|是| 查询报告的唯一编号<br> 长度在22以内的字符串，不可重复<br>|
|name|String|是| 姓名<br>|
|idCard|String|是| 身份证号<br>|
|useIdleTime|Boolean|否| 是否使用闲时队列查询任务<br>|
|authFileImage|byte[]|是| 扫描件图片<br>|
|idCardImage|byte[]|是| 身份证图片<br>|
|authFileHash|String|是| 扫描件图片哈希码<br>|
|idCardHash|String|是| 身份证图片哈希码<br>|
|creditAuthImage|byte[]|否| 授权书照片<br>|
|fileWithPersonImage|byte[]|否| 本人手持授权书照片<br>|
|otherImage|byte[]|否| 备用照片<br>|
|account|String|是|银行卡号|

#### 业务数据（t）说明

|属性名|类型|说明|
|--|--|--|
|status|Status| 提交任务状态，取值：ADD_NEW_TASK / DUPLICATE_TASK / HISTORY_RECORD，分别表示新增查询任务、重复提交任务、已有可用记录。|

#### 返回码说明
|success|code|说明|备注|
|--|--|--|--|
|TRUE|L0000|提交成功|任务提交成功，可以继续调用查询报告|
|FALSE|L0002|业务方token没有当前调用接口的权限|联系对接方处理|
|FALSE|L0003|业务方token不合法|联系对接方处理|
|FALSE|L0004|参数校验失败|修改参数重新提交任务|
|FALSE|L0005|调用方ip白名单验证未通过|联系对接方处理|
|FALSE|L0006|业务方接口配置出错|联系对接方处理|
|FALSE|L0009|第三方调用失败或征信内部错误|联系对接方处理|
