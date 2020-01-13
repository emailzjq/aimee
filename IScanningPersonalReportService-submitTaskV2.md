#  提交扫描件查询征信报告2.0任务
### com.yooli.zixin.intf.IScanningPersonalReportService.submitTaskV2

## 版本历史

|文档版本|变更时间|变更人|属性|
|--|--|--|--|
|V1.0|2019-04-10|yooli|新增|

## 依赖地址
Maven：
```xml
<dependency>
    <groupId>credit-yooli</groupId>
    <artifactId>credit-zixin-intf</artifactId>
    <version>5.2.2</version>
</dependency>
```

## 调用说明
征信平台dubbo远程服务的调用方法和解析规则请参照 **基础数据类型和约定** 中的方案进行处理。

## 消费配置
版本：1.0.0
超时时间：建议为10秒
重试次数：建议为0
配置文件示例：
```xml
<dubbo:registry protocol="zookeeper" address="172.16.2.158:2181"/>
<dubbo:consumer timeout="10000" retries="0" check="false"/>

<dubbo:reference interface="com.yooli.zixin.intf.IScanningPersonalReportService"
                 id="IScanningPersonalReportService" version="1.0.0"/>
```

## 接口说明

##### 请求参数


数据类型：`ScanningPersonalReportRequestDto`对象

|属性名|类型|是否必要|说明|
|--|--|--|--|
|token|String|是|征信平台分配给业务线的账号，测试环境为yooli|
|creditOrderId|String|是|请求进件号，唯一的字符串|
|messageId|String|是| 查询报告的唯一编号<br> 长度在22以内的字符串，不可重复<br>|
|name|String|是| 姓名<br>|
|idCard|String|是| 身份证号<br>|
|useIdleTime|Boolean|否| 是否使用闲时队列查询任务<br>|
|authFileImage|byte[]|是| 扫描件图片<br>|
|idCardImage|byte[]|是| 身份证图片<br>|
|authFileHash|String|是| 扫描件图片哈希码<br>|
|authFileImageType|String|否| 查征授权书扫描件类型（IMG/PDF）,默认IMG<br>|
|idCardHash|String|是| 身份证图片哈希码<br>|
|creditAuthImage|byte[]|否| 授权书照片<br>|
|fileWithPersonImage|byte[]|否| 本人手持授权书照片<br>|
|otherImage|byte[]|否| 备用照片<br>|

##### 返回值

|属性名|类型|说明|
|--|--|--|
|serialNo|String|征信平台流水号，用来标识此次调用，该值唯一|
|code|String|返回码，用来标识此次调用的结果|
|message|String|返回结果描述，用来对返回结果码进行解释说明|
|success|boolean|返回调用成功状态，表示第三方是否返回了足以进行下一步业务处理的内容，与具体业务无关|
|t|Object|业务数据，在调用成功且查得的情况下该值非空|

##### 泛型返回值及其成员



数据类型：`SubmitTaskResponseDto`

|属性名|类型|说明|
|--|--|--|
|status|Status| 提交任务状态<br>|

##### 调用示例
```java
//补充
```




