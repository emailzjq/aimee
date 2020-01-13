#  扫描件查询用户征信报告2.0银行卡版

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
### 资信扫描件查询报告获取结果
#### 调用https接口接入
生产地址：  
https://credit.szguoyinshengda.com/credit/zixin/getScanningReportV2ByAccount  
测试地址：  
https://credit-test.szguoyinshengda.com/credit/zixin/getScanningReportV2ByAccount  
请求方式：POST  
请求参数格式：json字符串  
返回格式及编码：application/json; charset=utf-8

##### 请求参数

|属性名|类型|是否必要|说明|
|--|--|--|--|
|token|String|是|国银分配给业务线的账号|
|creditOrderId|String|是|请求进件号，唯一的字符串|
|name|String|是| 被查询人姓名<br>|
|idCard|String|是| 被查询人身份证号<br>|
|account|String|是|被查人银行卡号|

##### 泛型返回值（t）及其成员

数据类型：`PersonalReportResponseDtoV2`

|属性名|类型|说明|
|--|--|--|
|reportHead|ReportHead| 报告头信息<br>|
|baseInfo|BaseInfoV2| 个人基本信息<br>|
|reportSummary|ReportSummary| 信息概要<br>|
|creditTranDetailsInfo|CreditTranDetailsInfo| 信贷交易信息明细<br>|
|nonCreditTranDetailsInfo|NonCreditTranDetailsInfo| 非信贷交易信息明细<br>|
|publicInfo|PublicInfoV2| 公共信息明细<br>|
|userDeclare|List&lt;AnnotationInfo&gt;| 本人声明<br>|
|objLabel|List&lt;AnnotationInfo&gt;| 异议标注<br>|
|queryInfo|List&lt;QueryInfo&gt;| 查询记录<br>|
|rptExplain|TitleAndContent| 报告说明<br>|
|htmlReport|String| BASE64编码后的html报告<br>|
|pdfReport|String| BASE64编码后的pdf报告<br>|



数据类型：`ReportHead`

|属性名|类型|说明|
|--|--|--|
|reportIdentInfo|ReportIdentityInfo| 报告标识信息段<br>|
|thisQueryReqInfo|ThisQueryReqInfo| 本次查询请求信息段<br>|
|otherIdInfo|List&lt;OtherIdInfo&gt;| 其他证件信息段<br>|
|antiFraudWarnInfo|AntiFraudWarnInfo| 防欺诈警示信息段<br>|
|objPromptMsg|ObjPromptMsg| 异议提示信息段<br>|



数据类型：`ReportIdentityInfo`

|属性名|类型|说明|
|--|--|--|
|reportId|String| 报告编号<br>|
|reportTime|String| 报告时间<br>|



数据类型：`ThisQueryReqInfo`

|属性名|类型|说明|
|--|--|--|
|queryName|String| 被查人姓名<br>|
|queryCertType|String| 被查人证件类型<br>|
|queryCredNum|String| 被查人证件号码<br>|
|queryOrg|String| 查询机构<br>|
|queryReasonCode|String| 查询原因<br>|



数据类型：`OtherIdInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|type|String| 证件类型<br>|
|idCard|String| 证件号码<br>|



数据类型：`AntiFraudWarnInfo`

|属性名|类型|说明|
|--|--|--|
|sign|String| 防欺诈警示标识<br>|
|startTime|String| 防欺诈警示生效日期<br>|
|endTime|String| 防欺诈警示截止日期<br>|



数据类型：`ObjPromptMsg`

|属性名|类型|说明|
|--|--|--|
|info|String| 异议信息提示<br>|



数据类型：`BaseInfoV2`

|属性名|类型|说明|
|--|--|--|
|identityInfo|IdentityInfo| 身份信息<br>|
|spouseInfo|SpouseInfo| 配偶信息<br>|
|resideInfo|List&lt;ResideInfo&gt;| 居住信息<br>|
|occupationInfo|List&lt;OccupationInfo&gt;| 职业信息<br>|



数据类型：`IdentityInfo`

|属性名|类型|说明|
|--|--|--|
|gender|String| 性别<br>|
|dateOfBirth|String| 出生日期<br>|
|maritalStatus|String| 婚姻状况<br>|
|mobilePhone|String| 手机号码<br>|
|companyPhone|String| 单位电话<br>|
|homePhone|String| 住宅电话<br>|
|education|String| 学历<br>|
|degree|String| 学位<br>|
|contactAddress|String| 通讯地址<br>|
|residenceAddress|String| 户籍地址<br>|



数据类型：`SpouseInfo`

|属性名|类型|说明|
|--|--|--|
|spouseName|String| 配偶姓名<br>|
|spouseCertType|String| 配偶证件类型<br>|
|spouseCredNum|String| 配偶证件号码<br>|
|spouseCompany|String| 配偶工作单位<br>|
|spousePhone|String| 配偶联系电话<br>|



数据类型：`ResideInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|resideAddr|String| 居住地址<br>|
|residePhone|String| 住宅电话<br>|
|resideStatus|String| 居住状况<br>|
|infoUpdateDate|String| 信息更新日期<br>|



数据类型：`OccupationInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|companyName|String| 工作单位<br>|
|companyAddress|String| 单位地址<br>|
|occupation|String| 职业<br>|
|companyType|String| 单位性质<br>|
|companyPhone|String| 单位电话<br>|
|position|String| 职务<br>|
|postTitle|String| 职称<br>|
|employedYear|String| 进入单位年份<br>|
|infoUpdateDate|String| 信息更新日期<br>|
|industry|String| 行业<br>|



数据类型：`BaseInfo`

|属性名|类型|说明|
|--|--|--|
|creditPrtlIdent|String| 授信协议标识<br>|
|managmtOrg|String| 管理机构<br>|
|accountId|String| 账户标识<br>|
|issuanceDate|String| 开立日期<br>|
|dueDate|String| 到期日期<br>|
|money|String| 借款金额<br>|
|currency|String| 账户币种<br>|
|type|String| 业务类型<br>|
|guratMode|String| 担保方式<br>|
|repayPerid|String| 还款期数<br>|
|repayFrequency|String| 还款频率<br>|
|repayType|String| 还款方式<br>|
|commonBwMark|String| 共同借款标志<br>|



数据类型：`ReportSummary`

|属性名|类型|说明|
|--|--|--|
|perCredRptNum|PerCredRptNum| 个人信用报告数字解读<br>|
|creditTranPromptInfo|List&lt;CreditTranPromptInfo&gt;| 信贷交易提示信息<br>|
|creditDefaultSumInfo|CreditDefaultSumInfo| 信贷交易违约信息概要<br>|
|creditTranAndDebtSummInfo|CreditTranAndDebtSummInfo| 信贷交易授信及负债信息概要<br>|
|nonCreditTranSummInfo|NonCreditTranSummInfo| 非信贷交易信息概要<br>|
|publicSummInfo|PublicSummInfo| 公共信息概要<br>|
|queryRecordSummary|QueryRecordSummary| 查询记录概要<br>|



数据类型：`PerCredRptNum`

|属性名|类型|说明|
|--|--|--|
|number|String| 数字解读<br>|
|rePosition|String| 相对位置<br>|
|explain|String| 说明<br>|



数据类型：`CreditTranPromptInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|businessType|String| 业务类别<br>|
|accountNum|String| 账户数<br>|
|firstBusinessReleaseMonth|String| 首笔业务发放月份<br>|



数据类型：`CreditDefaultSumInfo`

|属性名|类型|说明|
|--|--|--|
|beRecoverySummInfo|List&lt;BeRecoverySummInfo&gt;| 被追偿信息汇总<br>|
|badDebtsSummInfo|BadDebtsSummInfo| 呆账信息汇总<br>|
|overdueSummInfo|List&lt;OverdueSummInfo&gt;| 逾期（透支）信息汇总<br>|



数据类型：`BeRecoverySummInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|type|String| 业务类型<br>|
|accountNum|String| 账户数<br>|
|balance|String| 余额<br>|



数据类型：`BadDebtsSummInfo`

|属性名|类型|说明|
|--|--|--|
|accountNum|String| 账户数<br>|
|balance|String| 余额<br>|



数据类型：`OverdueSummInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|accountType|String| 账户类型<br>|
|accountNum|String| 账户数<br>|
|numMonth|String| 月份数<br>|
|maxMonthlyTotalOverdue|String| 单月最高逾期/透支总额<br>|
|longestOverdueMonths|String| 最长逾期/透支预算<br>|



数据类型：`CreditTranAndDebtSummInfo`

|属性名|类型|说明|
|--|--|--|
|nonRevolvingLoanSummInfo|LoanSummInfo| 非循环贷款账户信息汇总<br>|
|revolvingQuotaLoanSummInfo|LoanSummInfo| 循环额度下分账户信息汇总<br>|
|revolvingLoanAccountSummInfo|LoanSummInfo| 循环贷账户信息汇总<br>|
|debitCardAccountSummInfo|DebitCardAccountSummInfo| 贷记卡账户信息汇总<br>|
|quasiDebitCardSummInfo|QuasiDebitCardSummInfo| 准贷记卡账户信息汇总<br>|
|repayLibtySummInfo|RepayLibtySummInfo| 相关还款责任信息汇总<br>|



数据类型：`LoanSummInfo`

|属性名|类型|说明|
|--|--|--|
|orgNum|String| 管理机构数<br>|
|accountNum|String| 账户数<br>|
|authorizationTotal|String| 授信总数<br>|
|balance|String| 余额<br>|
|avgRepaymentLastSixMonth|String| 六个月平均应还款<br>|



数据类型：`DebitCardAccountSummInfo`

|属性名|类型|说明|
|--|--|--|
|orgNum|String| 发卡机构数<br>|
|accountNum|String| 账户数<br>|
|authorizationTotal|String| 授信总额<br>|
|maxCreditSingleBank|String| 单家机构最高授信额<br>|
|minCreditSingleBank|String| 单家机构最低授信额<br>|
|usedQuota|String| 已用额度<br>|
|avgUsageQuotaLastSixMonth|String| 最近6 个月平均使用额度<br>|



数据类型：`QuasiDebitCardSummInfo`

|属性名|类型|说明|
|--|--|--|
|orgNum|String| 发卡机构数<br>|
|accountNum|String| 账户数<br>|
|authorizationTotal|String| 授信总额<br>|
|maxCreditSingleBank|String| 单家机构最高授信额<br>|
|minCreditSingleBank|String| 单家机构最低授信额<br>|
|overdraftBalance|String| 透支余额<br>|
|avgUsageQuotaLastSixMonth|String| 最近6 个月平均使用额度<br>|



数据类型：`RepayLibtySummInfo`

|属性名|类型|说明|
|--|--|--|
|type|String| 相关还款责任信息类型<br>|
|guaraLibtyAccountNum|String|担保责任账户数<br>|
|guaraLibtyAccountMoney|String|担保责任金额<br>|
|guaraLibtyAccountBalance|String|担保责任余额<br>|
|otherLibtyAccountNum|String|其他相关还款责任账户数<br>|
|otherLibtyAccountMoney|String|其他相关还款责任金额<br>|
|otherLibtyAccountBalance|String|其他相关还款责任余额<br>|



数据类型：`NonCreditTranSummInfo`

|属性名|类型|说明|
|--|--|--|
|postPaidBusinessArrearsSummInfo|List&lt;PostPaidBusinessArrearsSummInfo&gt;| 后付费业务欠费信息汇总<br>|



数据类型：`PostPaidBusinessArrearsSummInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|postPaidBusinessType|String| 后付费业务类型<br>|
|numArrearsAccount|String| 欠费账户数<br>|
|amountOwed|String| 欠费金额<br>|



数据类型：`PublicSummInfo`

|属性名|类型|说明|
|--|--|--|
|publicInfo|List&lt;PublicInfo&gt;| 公共信息汇总<br>|



数据类型：`PublicInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|publicInfoType|String| 公共信息类型<br>|
|numRecoeds|String| 记录数<br>|
|moneyInvolved|String| 涉及金额<br>|



数据类型：`QueryRecordSum`

|属性名|类型|说明|
|--|--|--|
|lastOneMonthOrgLoanApprovalSum|String| 最近一个月内贷款审批查询机构数<br>|
|lastOneMonthOrgCreditCardApprovalSum|String| 最近一个月内信用卡审批查询机构数<br>|
|lastOneMonthLoanApprovalSum|String| 最近一个月内贷款审批查询次数<br>|
|lastOneMonthCreditCardApprovalSum|String| 最近一个月内信用卡审批查询次数<br>|
|lastOneMonthSelfQuerySum|String| 最近一个月内本人查询次数<br>|
|lastTwoYearsLoanMangeSum|String| 最近两年内贷后管理查询次数<br>|
|lastTwoYearsGuarApproSum|String| 最近两年内担保资格审查查询次数<br>|
|lastTwoYearSpeMerchApproSum|String| 最近两年内特约商户实名审查查询次数<br>|



数据类型：`QueryRecordSummary`

|属性名|类型|说明|
|--|--|--|
|lastQueryRecordInfo|LastQueryRecordInfo| 上一次查询记录信息<br>|
|queryRecordSummInfo|QueryRecordSummInfo| 查询记录汇总信息<br>|
|objectionAndExplainInfo|ObjectionAndExplainInfo| 异议及说明信息<br>|



数据类型：`LastQueryRecordInfo`

|属性名|类型|说明|
|--|--|--|
|lastQueryDate|String| 上一次查询日期<br>|
|lastQueryOrg|String| 上一次查询机构<br>|
|lastQueryReason|String| 上一次查询原因<br>|



数据类型：`QueryRecordSummInfo`

|属性名|类型|说明|
|--|--|--|
|numQueryOrgLoanApprovalLastOneMonth|String| 最近1个月内的查询机构数（贷款审批）<br>|
|numQueryOrgCreditCardApprovalLastOneMonth|String| 最近1个月内的查询机构数（信用卡审批）<br>|
|numQueryLoanApprovalLastOneMonth|String| 最近1个月内的查询次数（贷款审批）<br>|
|numQueryCreditCardApprovalLastOneMonth|String| 最近1个月内的查询次数（信用卡审批）<br>|
|numQuerySelfQueryLastOneMonth|String| 最近1个月内的查询次数（本人查询）<br>|
|numQueryPostLoanManagementLastTwoYear|String| 最近2年内的查询次数（贷后管理）<br>|
|numQueryGuaranteeQualificationReviewLastTwoYear|String| 最近2年内的查询次数（担保资格审查）<br>|
|numQuerySpecialMerchantRealNameReviewLastTwoYear|String| 最近2年内的查询次数（特约商户实名审查）<br>|



数据类型：`ObjectionAndExplainInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|objectionLabel|String| 异议标注<br>|
|addDate|String| 添加时间<br>|



数据类型：`CreditTranDetailsInfo`

|属性名|类型|说明|
|--|--|--|
|beRecoveryDetailsInfo|List&lt;BeRecoveryDetailsInfo&gt;| 被追偿信息<br>|
|nonrevolvingLoanDetailnfo|List&lt;NonrevolvingLoanDetailnfo&gt;| 非循环贷账户<br>|
|loopQuotaSubAct|List&lt;LoopQuotaSubAct&gt;| 循环额度下分账户<br>|
|revolvinLoanAct|List&lt;RevolvinLoanAct&gt;| 循环贷账户<br>|
|creditCardAct|List&lt;CreditCardAct&gt;| 贷记卡账户<br>|
|semiCreditCardAct|List&lt;SemiCreditCardAct&gt;| 准贷记卡账户<br>|
|relvRepayRsbltyInfo|RelvRepayRsbltyInfo| 相关还款责任信息<br>|
|creditPrtlInfo|List&lt;CreditPrtlInfo&gt;| 授信协议信息<br>|



数据类型：`BeRecoveryDetailsInfo`

|属性名|类型|说明|
|--|--|--|
|baseInfo|BeRecoveryDetailBaseInfo| 基本信息<br>|
|latestPerformanceInfo|LatestPerformanceInfo| 最新表现信息<br>|
|specialTranInfo|List&lt;SpecialTranInfo&gt;| 特殊交易信息<br>|
|annotationInfo|List&lt;AnnotationInfo&gt;| 标注及声明<br>|



数据类型：`BeRecoveryDetailBaseInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|managmtOrg|String| 管理机构<br>|
|type|String| 业务种类<br>|
|receiveDate|String| 债权接收日期<br>|
|money|String| 债权金额<br>|
|status|String| 债权转移时的还款状态<br>|



数据类型：`LatestPerformanceInfo`

|属性名|类型|说明|
|--|--|--|
|title|String| 最新表现信息标题<br>|
|accountStatus|String| 账户状态<br>|
|closeDate|String| 关闭日期<br>|
|month|String| 转出月份<br>|
|balance|String| 余额<br>|
|lastRepayDate|String| 还款日期/最近一次还款日期<br>|
|lastRepayMoney|String| 还款金额/最近一次还款金额<br>|
|fiveClass|String| 五级分类<br>|
|repayStatus|String| 还款状态<br>|



数据类型：`SpecialTranInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|type|String| 特殊交易类型<br>|
|businessData|String| 发生日期<br>|
|changeMonth|String| 变更月数<br>|
|money|String| 发生金额<br>|
|detailInfo|String| 明细记录<br>|



数据类型：`AnnotationInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|type|String| 类型<br> 机构说明 / 本人声明 / 异议标注 / 特殊标注<br>|
|content|String| 声明<br>|
|addDate|String| 添加日期<br>|



数据类型：`NonrevolvingLoanDetailnfo`

|属性名|类型|说明|
|--|--|--|
|baseInfo|BaseInfo| 基本信息<br>|
|latestPerformanceInfo|LatestPerformanceInfo| 最新表现信息<br>|
|latestMonPerfmInfo|LatestMonPerfmInfo| 最近一次月度表现信息<br>|
|last5YearsHisPerfmInfo|TitleAndContent| 最近五年内历史表现信息<br>|
|specialEvenInfo|ContentAndNo| 特殊事件说明<br>|
|specialTranInfo|List&lt;NonrevolvingSpecialTranInfo&gt;| 特殊交易<br>|
|annotationInfo|List&lt;AnnotationInfo&gt;| 标注及声明<br>|



数据类型：`LatestMonPerfmInfo`

|属性名|类型|说明|
|--|--|--|
|dueDateInfo|String| 截止日期信息<br>|
|accountStatus|String| 账户状态（呆账）<br>|
|balance|String| 余额<br>|
|usedCreditLines|String| 已用额度<br>|
|noIsdLargeSpeBalance|String| 未出单的大额专项分期余额<br>|
|fiveClass|String| 五级分类<br>|
|remainingRepaymentPeriod|String| 剩余还款期数<br>|
|repaymentDate|String| 应还款日<br>|
|thisMonthShouldRepayment|String| 本月应还款<br>|
|actualRepaymentThisMonth|String| 本月实还款<br>|
|lastRepaymentDate|String| 最近一次还款日期<br>|
|numCurrentOverduePeriods|String| 当前逾期期数<br>|
|currentOverdueTotal|String| 当前逾期总额<br>|
|overdue31To60DaysWithoutRepaymentOfPrincipal|String| 逾期31—60天未还本金<br>|
|overdue61To90DaysWithoutRepaymentOfPrincipal|String| 逾期61－90天未还本金<br>|
|overdue91To180DaysWithoutRepaymentOfPrincipal|String| 逾期91－180天未还本金<br>|
|overduePaymentOfMoreThan180Days|String| 逾期180天以上未还本金<br>|
|unpaidMoneyOf180Days|String| 透支180天以上未付金额<br>|
|avgUsedOfSixMonth|String| 最近6个月平均使用额度<br>|
|avgOverOfSixMonth|String| 最近6个月平均透支余额<br>|
|maxUsed|String| 最大使用额度<br>|
|maxOver|String| 最大透支余额<br>|



数据类型：`TitleAndContent`

|属性名|类型|说明|
|--|--|--|
|title|String| 近60个月还款记录标题<br>|
|content|String| 近60个月还款状态及金额，格式为状态金额|状态金额，按时间降序（最新的在前）<br>|



数据类型：`Content`

|属性名|类型|说明|
|--|--|--|
|content|String| 内容<br>|



数据类型：`ContentAndNo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|content|String| 内容<br>|



数据类型：`NonrevolvingSpecialTranInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|type|String| 特殊交易类型<br>|
|businessData|String| 发生日期<br>|
|changeMonth|String| 变更月数<br>|
|money|String| 发生金额<br>|
|detailInfo|String| 明细记录<br>|



数据类型：`LoopQuotaSubAct`

|属性名|类型|说明|
|--|--|--|
|baseInfo|BaseInfo| 基本信息<br>|
|latestPerformanceInfo|LatestPerformanceInfo| 最新表现信息<br>|
|latestMonPerfmInfo|LatestMonPerfmInfo| 最近一次月度表现信息<br>|
|last5YearsHisPerfmInfo|TitleAndContent| 最近五年内历史表现信息<br>|
|specialTranInfo|List&lt;SpecialTranInfo&gt;|  特殊交易<br>|
|annotationInfo|List&lt;AnnotationInfo&gt;| 标注及声明<br>|



数据类型：`RevolvinLoanAct`

|属性名|类型|说明|
|--|--|--|
|baseInfo|BaseInfo| 基本信息<br>|
|latestPerformanceInfo|LatestPerformanceInfo| 最新表现信息<br>|
|latestMonPerfmInfo|LatestMonPerfmInfo| 最近一次月度表现信息<br>|
|last5YearsHisPerfmInfo|TitleAndContent| 最近五年内历史表现信息<br>|
|specialTranInfo|List&lt;SpecialTranInfo&gt;| 特殊交易<br>|
|annotationInfo|List&lt;AnnotationInfo&gt;| 标注及声明<br>|



数据类型：`CreditCardAct`

|属性名|类型|说明|
|--|--|--|
|baseInfo|BaseInfo| 基本信息<br>|
|latestPerformanceInfo|LatestPerformanceInfo| 最新表现信息<br>|
|latestMonPerfmInfo|LatestMonPerfmInfo| 最近一次月度表现信息<br>|
|largeAmtSpeclStgdInfo|CreditCardLargeAmtSpeclStgdInfo| 大额专项分期信息<br>|
|last5YearsHisPerfmInfo|TitleAndContent| 最近五年内历史表现信息<br>|
|specialEvents|ContentAndNo| 特殊事件说明<br>|
|specialTranInfo|List&lt;SpecialTranInfo&gt;| 特殊交易<br>|
|annotationInfo|List&lt;AnnotationInfo&gt;| 标注及声明<br>|



数据类型：`CreditCardLargeAmtSpeclStgdInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|lines|String| 大额专项分期额度<br>|
|beginDate|String| 分期额度生效日期<br>|
|dueDate|String| 分期额度到期日期<br>|
|usedLines|String| 已用分期金额<br>|



数据类型：`SemiCreditCardAct`

|属性名|类型|说明|
|--|--|--|
|baseInfo|SemiCreditCardBaseInfo| 基本信息<br>|
|latestPerformanceInfo|LatestPerformanceInfo| 最新表现信息<br>|
|latestMonPerfmInfo|LatestMonPerfmInfo| 最近一次月度表现信息<br>|
|last5YearsHisPerfmInfo|TitleAndContent| 最近五年内历史表现信息<br>|
|specialTranInfo|List&lt;SpecialTranInfo&gt;| 特殊交易信息<br>|
|annotationInfo|List&lt;AnnotationInfo&gt;| 标注及声明<br>|



数据类型：`SemiCreditCardBaseInfo`

|属性名|类型|说明|
|--|--|--|
|creditPrtlIdent|String| 授信协议标识<br>|
|org|String| 发卡机构<br>|
|accountId|String| 账户标识<br>|
|issuanceDate|String| 开立日期<br>|
|lines|String| 账户授信额度<br>|
|shareLines|String| 共享授信额度<br>|
|currency|String| 币种<br>|
|guratMode|String| 担保方式<br>|



数据类型：`RelvRepayRsbltyInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|objectType|String| 业务对象类型<br>|
|org|String| 管理机构<br>|
|businessType|String| 业务种类<br>|
|openingDate|String| 开立日期<br>|
|expireDate|String| 到期日期<br>|
|type|String| 责任人类型<br>|
|money|String| 还款责任金额<br>|
|currency|String| 币种<br>|
|guaraContractNum|String| 保证合同编号<br>|
|dueDateInfo|String| 截止日期信息<br>|
|balance|String| 余额<br>|
|fiveClass|String| 五级分类<br>|
|repayStatus|String| 还款状态<br>|
|dueMonths|String| 逾期月数<br>|



数据类型：`CreditPrtlInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 授信协议编号<br>|
|org|String| 管理机构<br>|
|creditAgreementIdent|String| 授信协议标识<br>|
|effectiveDate|String| 生效日期<br>|
|expireDate|String| 到期日期<br>|
|creditLineUsage|String| 授信额度用途<br>|
|creditLine|String| 授信额度<br>|
|limit|String| 授信限额<br>|
|limitNo|String| 授信限额编号<br>|
|used|String| 已用额度<br>|
|currency|String| 币种<br>|



数据类型：`NonCreditTranDetailsInfo`

|属性名|类型|说明|
|--|--|--|
|postPaidBusinessInfo|PostPaidBusinessInfo| 后付费记录<br>|



数据类型：`PostPaidBusinessInfo`

|属性名|类型|说明|
|--|--|--|
|baseInfo|PostPaidBusinessBaseInfo| 基本信息<br>|
|last2YearsHisInfo|TitleAndContent| 近两年表现信息<br>|



数据类型：`PostPaidBusinessBaseInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|orgName|String| 机构名称<br>|
|businessType|String| 业务类型<br>|
|businessOpenDate|String| 业务开通日期<br>|
|currentPaymentStatus|String| 当前缴费状态<br>|
|currentArrearsAmount|String| 当前欠费金额<br>|
|billDate|String| 记账年月<br>|



数据类型：`PublicInfoV2`

|属性名|类型|说明|
|--|--|--|
|taxInfo|List&lt;TaxInfo&gt;| 欠税记录<br>|
|civilJudgmentRecord|List&lt;CivilJudgmentRecord&gt;| 民事判决记录<br>|
|enforceRecord|List&lt;EnforceRecord&gt;| 强制执行记录<br>|
|admPenaltyRecord|List&lt;AdmPenaltyRecord&gt;| 行政处罚记录<br>|
|hosFundPayRecord|List&lt;HosFundPayRecord&gt;| 住房公积金参缴记录<br>|
|subReliefRecord|List&lt;SubReliefRecord&gt;| 低保救助记录<br>|
|practiceQuaRecord|List&lt;PracticeQuaRecord&gt;| 执业资格记录<br>|
|admRewardRecord|List&lt;AdmRewardRecord&gt;| 行政奖励记录<br>|



数据类型：`TaxInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|taxAuthorities|String| 主管税务机关<br>|
|totalTaxOwed|String| 欠税总额<br>|
|taxOwedDate|String| 欠税统计日期<br>|



数据类型：`CivilJudgmentRecord`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|courtFiling|String| 立案法院<br>|
|caseReason|String| 案由<br>|
|caseDate|String| 立案日期<br>|
|closeCaseMode|String| 结案方式<br>|
|judgmentResult|String| 判决/调解结果<br>|
|judgmentResultEffectiveDate|String| 判决/调解生效日期<br>|
|litigationTarget|String| 诉讼标的<br>|
|amountLitigation|String| 诉讼标的金额<br>|



数据类型：`EnforceRecord`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|executiveCourt|String| 执行法院<br>|
|executionReason|String| 执行案由<br>|
|caseDate|String| 立案日期<br>|
|closeCaseMode|String| 结案方式<br>|
|caseStatus|String| 案件状态<br>|
|closeCaseDate|String| 结案日期<br>|
|applyForExecuteObject|String| 申请执行标的<br>|
|applyForExecutedObjectAmount|String| 申请执行标的金额<br>|
|executedObject|String| 已执行标的<br>|
|executedObjectAmount|String| 已执行标的金额<br>|



数据类型：`AdmPenaltyRecord`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|punishedAgency|String| 处罚机构<br>|
|punishedContent|String| 处罚内容<br>|
|amountPunished|String| 处罚金额<br>|
|punishedEffectiveDate|String| 生效日期<br>|
|punishedExpireDate|String| 截止日期<br>|
|result|String| 行政复议结果<br>|



数据类型：`HosFundPayRecord`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|paymentLocation|String| 参缴地<br>|
|paymentDate|String| 参缴日期<br>|
|firstPaymentMonth|String| 初缴月份<br>|
|payToMonth|String| 缴至月份<br>|
|paymentStatus|String| 缴费状态<br>|
|monthPayDeposit|String| 月缴存额<br>|
|personPayProportion|String| 个人缴存比例<br>|
|companyPayProportion|String| 单位缴存比例<br>|
|payCompany|String| 缴费单位<br>|
|infoUpdateDate|String| 信息更新日期<br>|



数据类型：`SubReliefRecord`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|personnelCategory|String| 人员类别<br>|
|location|String| 所在地<br>|
|workUnit|String| 工作单位<br>|
|familyMonthlyIncome|String| 家庭月收入<br>|
|applicationDate|String| 申请日期<br>|
|approvalDate|String| 批准日期<br>|
|infoUpdateDate|String| 信息更新日期<br>|



数据类型：`PracticeQuaRecord`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|name|String| 执业资格名称<br>|
|rank|String| 等级<br>|
|getDate|String| 获得日期<br>|
|expireDate|String| 到期日期<br>|
|revocationDate|String| 吊销日期<br>|
|issuingAgency|String| 颁发机构<br>|
|institutionLocated|String| 机构所在地<br>|



数据类型：`AdmRewardRecord`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|rewardInstitution|String| 奖励机构<br>|
|rewardContent|String| 奖励内容<br>|
|effectiveDate|String| 生效日期<br>|
|expireDate|String| 截止日期<br>|



数据类型：`QueryInfo`

|属性名|类型|说明|
|--|--|--|
|no|String| 编号<br>|
|queryDate|String| 查询日期<br>|
|queryOrg|String| 查询机构<br>|
|reason|String| 查询原因<br>|



#### 返回码说明
|success|code|说明|备注|
|--|--|--|--|
|TRUE|L0000|查询第三方成功且查得结果|获取到客户报告，收费。此时三方反馈码为0000|
|FALSE|L0002|业务方token没有当前调用接口的权限|联系对接方处理|
|FALSE|L0003|业务方token不合法|联系对接方处理|
|FALSE|L0004|参数校验失败|修改参数重新提交任务|
|FALSE|L0005|调用方ip白名单验证未通过|联系对接方处理|
|FALSE|L0006|业务方接口配置出错|联系对接方处理|
|FALSE|L0009|第三方调用失败或征信内部业务失败|联系对接方处理|
|FALSE|L0011|提交任务成功，还未获取第三方结果|一段时间后重新获取报告（提交材料仍在审批中、审批通过还未获取到报告结果）|
|FALSE|L0012|未发现对应的任务|重新提交任务后再获取数据|
|FALSE|-402|征信调用第三方超时触发服务降级|重新获取报告|
|FALSE|-403|征信调用第三方频繁失败触发熔断|联系对接方处理|
|FALSE|其他|第三方返回码（异常情况）或http异常码|1.返回码具体参考三方反馈码，均不收费。2.若需要重新获取报告，则需再次重新提交任务3.白户（0019）不建议短期内再次提交提交任务&获取报告|

##### 第三方反馈码（其他）

###### 资信系统返回码
|返回码|描述|
|--|--|
|0000|成功，不会出现，封装为L0000返回|
|0001|入库错误，退回|
|0002|征信报告查询失败|
|0003|请求报文有误|
|0004|报文头解析错误|
|0005|报文体格式错误|
|0006|查询申请有待审批|
|0008|该金融机构未签接口转换合同|
|0009|请求人行报告失败|
|0010|登陆人行账号密码错误|
|0011|登陆人行cookie失败|
|0012|人行服务器有误，信用报告查询出错！（人行没有查询记录）|
|0013|人行返回查询结果：信用报告查询出错！（人行没有查询记录）|
|0014|人行返回空报告！（人行没有查询记录）|
|0015|人行返回查询结果：查询各版本的信用报告说明异常！（人行没有查询记录）|
|0016|人行返回查询结果：获取数据库连接失败！（人行没有查询记录）|
|0017|人行返回查询结果：查询人证件号码无效！（人行没有查询记录）|
|0018|人行返回查询结果：查询人姓名不符合规范！（人行没有查询记录）|
|0019|人行返回查询结果：个人征信系统中没有此人的征信记录！（白户）|

###### 资信请求返回码
|返回码|描述|
|--|--|
|0100|请求报文不能为空|
|0101|解析请求报文失败|
|0102|非法交易吗TRADE_TYPE|
|0103|节点TRADE_TYPE不能为空|
|0106|申请金融机构代码不符|
|0108|申请操作用户无查询接口权限|
|0109|申请操作用户和密码不符|
|0110|解析人行返回报文失败|
|0111|人行返回特殊报告|
|0112|机构流水号MsgID重复|
|0113|根据交易流水号找不到对应的请求记录|
|0114|超时重新下载的报告，本地已删除|














