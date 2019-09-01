
## USSD
کد USSD یکی از خدمات ارزش افزوده‌ی پلتفرم پاد است. این سرویس یکی از رایج‌ترین راه‌ها برای پرداخت‌های خرد مردم است. با استفاده از این سرویس کاربران می‌توانند از تمامی مکان‌هایی که تلفن ‌همراه در آن‌جا آنتن دهد، به آسانی پرداخت‌های مرتبط با برنامه‌ی شما را انجام دهند.

<div class="box-end">
</div>
لیست کلی سرویس ها در جدول زیر آمده است: 

| ستون 1    | ستون 2                                       | ستون 3                                                                                                                         | ستون 4                         |
| --------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------ |
| نام سرویس | آدرس فراخوانی سرویس                          | کد **USSD**                                                                                                                    |
| **1**     | نمایش میزان موجودی  کیف پول کاربر            | **[ Server Address]/nzh/ussd/getCredit?cellphoneNumber=&wallet=PODLAND_WALLET&currencyCode=IRR**                               | **\*1*1#**                     |
| **2**     | نمایش میزان موجودی اصناف کاربر               | **[ Server Address ]/nzh/ussd/getBusinessCredit?cellphoneNumber=&guildId=**                                                    | **\*1_2_guildId#**             |
| **3**     | دریافت گزارش صورت حساب  در بازه زمانی دلخواه | **[ Server Address]/nzh/ussd/getAccountBill?cellphoneNumber=&wallet=&currencyCode=IRR** **&dateFrom=&dateTo=&size=5&offset=0** | **\*2*1#**                     |
| **4**     | درخواست برداشت وجه کل کیف پول پاد            | **[ Server Address ]/nzh/ussd/requestSettlement?cellphoneNumber=&wallet= PODLAND_WALLET&currencyCode= IRR**                    | **\*4_1_1#**                   |
| **5**     | درخواست برداشت وجه کیف پول پاد با مبلغ مشخص  | **[Serveraddress]/nzh/ussd/requestSettlement?cellphoneNumber=&wallet=PODLAND_WALLET** **&currencyCode= IRR &amount=**          | **\*4_1_2*amount#**            |
| **6**     | فعال کردن برداشت وجه خودکار کیف پول          | **[ ServerAddress]/nzh/ussd/addAutoSettlement?cellphoneNumber=&wallet=***\*&currencyCode= IRR**                                | **\*4*2#**                     |
| **7**     | غیر فعال کردن برداشت وجه خودکار کیف پول      | **[ Server Address]/nzh/ussd/removeAutoSettlement?cellphoneNumber=&wallet=PODLAND_WALLET&currencyCode=IRR**                    | **\*4*3#**                     |
| **8**     | دریافت لیست اصناف کسب و کار                  | **[ ServerAddress]/nzh/ussd/getGuildList?cellphoneNumber=&offset=0&size=5**                                                    | **\*4*4#**                     |
| **9**     | فعال کردن برداشت وجه خودکار صنف              | **[ Server Address]/nzh/ussd/addAutoSettlementForBusiness?cellphoneNumber=&guildId=***\*&currencyCode=IRR**                    | **\*4_guildId_1#**             |
| **10**    | غیر فعال کردن برداشت وجه خودکار صنف          | **[ ServerAddress]/nzh/ussd/removeAutoSettlementForBusiness?cellphoneNumber=&guildCode= &currencyCode=IRR**                    | **\*4*****guildCode***\*\*2#** |

<div class="box-end">
</div>

## سرویس نمایش میزان موجودی کیف پول کاربر

خروجی خام یا جیسان سرویس : 

    {
    
    "hasError": false,
    
    "referenceNumber":"345487",
    
    "errorCode":0,
    
    "count":0,
    
    "ott":"ca0b92d8d75301cc",
    
    "result":
    
    {
    
    "amount": 90000,
    
    "currencySrv":
    
    {
    
    "name":"ریال",
    
    "code":"IRR"
    
    },
    
    "isAutoSettle":false,
    
    "wallet":"PODLAND_WALLET",
    
    "active":true
    
    }
    
    }


خروجی مورد نیاز در  **USSD** : 

موجودی کیف پول شما مبلغ [amount]     [currencySrv.name]    میباشد .

<div class="box-end">
</div>

##    سرویس نمایش میزان موجودی اصناف مورد نظر کاربر

خروجی خام یا جیسان سرویس :

    {
    
    "hasError": false,
    
    "referenceNumber":"345606",
    
    "errorCode":0,
    
    "count": 0,
    
    "ott":"c2a48ffbd0f554c2",
    
    "result": {
    
    "customerAmountSrvs": [{
    
    "amount":900000,
    
    "currencySrv":{
    
    "name": "ریال",
    
    "code":"IRR"
    
    },
    
    "isAutoSettle":false,
    
    "wallet":"PODLAND_WALLET",
    
    "active":true
    
    }],
    
    "mainBusinessAmountSrvs": [{
    
    "amount": 20000,
    
    "withdrawableAmount":261,
    
    "guildSrv" : { 
    
    "id": 47,
    
    "name": "فناوری اطلاعات",
    
    "code":"INFORMATION_TECHNOLOGY_GUILD",
    
    "selected":false
    
    },
    
    "currencySrv": {
    
    "name":"ریال",
    
    "code":"IRR"
    
    },
    
    "isAutoSettle":false
    
    }],
    
    "blockedBusinessAmountSrvs": []
    
    }
    
    }

خروجی مورد نیاز در  **USSD** : 

میزان موجودی صنف    [mainBusinessAmountSrvs .guildSrv. name]  برابر با مبلغ  [mainBusinessAmountSrvs. amount]    [mainBusinessAmountSrvs. currencySrv.name] میباشد.

<div class="box-end">
</div>

## سرویس دریافت صورتحساب در بازه زمانی دلخواه تا حداکثر 5 گردش آخر

خروجی خام یا جیسان سرویس :

    }
    
    "hasError": false,
    
    "referenceNumber":
    "346272",
    
    "errorCode":
    0,
    
    "count": 3,
    
    "ott":
    "c663737ea8bacc06",
    
    "result" : [{
    
    "accountName": " ehsanmoshir
    "حساب,
    
    "issuanceDate":
    1535442438000,
    
    "amount": 5450,
    
    "debtor": false,
    
    "afterTxAmount":
    0,
    
    "description":
    "سند خرید کالا با اعتبار، در کسب و کار
    sa.zamani",
    
    "documentId": 4173,
    
    "txNumber":"-52365303497069219_1722_172.16.110.77_172.16.110.76#1535442209830",
    
    "issuerName": "احسان مشیر",
    
    "canceled":
    false,
    
    "currency": {
    
    "name":"ریال"
    
    "code": "IRR"
    
    {
    
    {,
    
    }                      
    
    "accountName":
    " ehsanmoshir  " حساب,
    
    "issuanceDate": 1535442438000,
    
    "amount": 5450,
    
    "debtor": true,
    
    "afterTxAmount": 5450,
    
    "description":
    "سند افزایش اعتبار کاربر از تفویض اعتبار جهت پرداخت در کسب و کار sa.zamani",            "documentId": 4172,
    
    txNumber":
    "-952365303497069219_1722_172.16.110.77_172.16.110.76#1535442209830",
    
    "issuerName": "احسان مشیر",
    
    "canceled": false,
    
    "currency" :}   
    
    "name":"ریال"
    
    "code":
    "IRR"
    
    { 
    
    {,

خروجی مورد نیاز در  **USSD**  در صورت عدم خطا:

**5 گردش آخر حساب از طریق پیامک به شمااعلام می گردد**

این بخش به دلیل طولانی بودن کاراکتر به صورت پیامک مورد نیاز میباشد.

صورتحساب صنف شما به شرح زیر میباشد:

1."  [description]  به مبلغ [amount] در تاریخ [issuanceDate]

2.  "[description]  به مبلغ [amount] در تاریخ [issuanceDate]

3. " [description]  به مبلغ [amount] در تاریخ [issuanceDate]

4.  ....

5.  ……

نکتــه مهم: فیــلد **debtor**   مشخص کننده بدهکار یا منفی بودن مبلغ میباشد که اگر **true** باشد میبایست عدد به شکل منفی نمایش داده شود.

<div class="box-end">
</div>

## سرویس درخواست برداشت وجه کامل کیف پول

خروجی خام یا جیسان سرویس:

    }
    
    "hasError":
    false,
    
    "referenceNumber": "346407",
    
    "errorCode": 0,
    
    "count": 0,
    
    "ott": "b134f21484ac0311",
    
    "result" : {
    
    "id": 629,
    
    "amount":
    50000,
    
    "requestDate":
    1537874517956,
    
    "customerProfileSrv" : {
    
    "version":
    6,
    
    "firstName": "",
    
    "lastName" : "",
    
    "name" : " ",
    
    "email":
    "",
    
    "nationalCode":
    "",
    
    "gender":
    "MAN_GENDER",
    
    "nickName"":
    
    "birthDate":
    551145600861,
    
    "followingCount":
    2,
    
    "profileImage":
    
    "joinDate":
    1530514009031,
    
    "cellphoneNumber":
    "",
    
    "userId":
    1722,
    
    "sheba":
    "",,
    
    "guest":
    false,
    
    "chatSendEnable":
    true,
    
    "chatReceiveEnable":
    true,
    
    "username":
    "ehsanmoshir",
    
    "ssoId":
    "",
    
    "ssoIssuerCode":
    1
    
    },
    
    "settleDate": 0,
    
    "status": "SETTLEMENT_REQUESTED",
    
    "currency" : {
    
    "name": "ریال",
    
    "code": "IRR"
    
    },
    
    "toolCode": "SETTLEMENT_TOOL_PAYA",
    
    "toolId": "",{{

خروجی مورد نیاز در  **USSD**:

 درخواست تسویه حساب کامل به مبلغ  [amount]  [currency.name] با موفقیت انجام شد. ( مبلغ سه رقم سه رقم جدا شود. )

<div class="box-end">
</div>

## سرویس درخواست برداشت وجه از کیف پول به مبلغ مشخص

خروجی خام یا جیسانسرویس :

    }
    
    "hasError": false,
    
    "referenceNumber": "346407",
    
    "errorCode": 0,
    
    "count": 0,
    
    "ott": "b134f21484ac0311",
    
    "result" : {
    
    "id": 629,
    
    "amount": 2000,
    
    "requestDate":1537874517956,
    
    "customerProfileSrv" : {
    
    "version":6,
    
    "firstName": "",
    
    "lastName" : "",
    
    "name" : " ",
    
    "email":"",
    
    "nationalCode":"",
    
    "gender": "MAN_GENDER",
    
    "nickName"":
    
    "birthDate":551145600861,
    
    "followingCount":2,
    
    "profileImage":
    
    "joinDate":1530514009031,
    
    "cellphoneNumber":"",
    
    "userId":1722,
    
    "sheba":"",,
    
    "guest":false,
    
    "chatSendEnable":true,
    
    "chatReceiveEnable":true,
    
    "username":"ehsanmoshir”,
    
    "ssoId":"",
    
    "ssoIssuerCode":1
    
    },
    
    "settleDate": 0,
    
    "status": "SETTLEMENT_REQUESTED",
    
    "currency" : {
    
    "name": "ریال",
    
    "code": "IRR"
    
    },
    
    "toolCode": "SETTLEMENT_TOOL_PAYA",
    
    "toolId": "",{{

خروجی مورد نیاز در  **USSD** : 

درخواست تسویه حساب به مبلغ  [amount]  [currency.name] با موفقیت انجام شد. مبلغ سه رقم سه رقم جدا شود.

<div class="box-end">
</div>

## سرویس درخواست فعال سازی برداشت وجه خودکار کیف پول

خروجی خام یا جیسان سرویس :

    }
    
    "hasError": false,
    
    "referenceNumber":"356276",
    
    "errorCode": 0,
    
    "count": 0,
    
    "ott": "b4bdd188981d9fac",
    
    "result": true
    
    {

خروجی مورد نیاز در  **USSD** : 

برداشت وجه خودکار از کیف پول فعال شد. 

    {
    
    "hasError": true,
    
    "referenceNumber":"356324",
    
    "errorCode": 999,
    
    "message":"این حساب شما در حال حاضر دارای تسویه حساب خودکارمی باشد",
    
    "count": 0,
    
    "ott":"51141ddadebe30ba"
    
    }

خروجی مورد نیاز در  **USSD** : 

    [message]

<div class="box-end">
</div>

## سرویس غیر فعال سازی برداشت وجه خودکار کیف پول

خروجی خام یا جیسان سرویس :

    }
    
    "hasError": false,
    
    "referenceNumber":"356276",
    
    "errorCode": 0,
    
    "count": 0,
    
    "ott": "b4bdd188981d9fac",
    
    "result": true
    
    {

خروجی مورد نیاز در  **USSD** : 

برداشت وجه خودکار کیف پول غیرفعال شد. 

    }
    
    "hasError": true,
    
    "referenceNumber": "356646",
    
    "errorCode": 999,
    
    "message "درخواست تسویه حساب خودکار یافت نشد":",
    
    "count": 0,
    
    "ott": "240973599b77583"
    
    {

خروجی مورد نیاز در  **USSD** : 

    [message]

<div class="box-end">
</div>

## سرویس دریافت لیست اصناف کسب و کار

خروجی خام یا جیسان سرویس :

    }
    
    "hasError": false,
    
    "referenceNumber": "359786",
    
    "errorCode": 0,
    
    "count": 6,
    
    "ott": "abbfeb2d25f1df86",
    
    "result:" [}
    
    "id": 47,
    
    "name” : “فناوری اطلاعات” , 
    
    "code": "INFORMATION_TECHNOLOGY_GUILD",
    
    "selected": false
    
    },
    
    {
    
    "id": 77,
    
    "name” : “بازی نویس” , 
    
    "code": "GAME_DEVELOPER_GUILD",
    
    "selected": false
    
    {,
    
    {
    
    "id": 51,
    
    "name” : “ورزش و تفریح و سرگرمی” , 
    
    "code": "ENTERTAINMENT_GUILD",
    
    "selected": false
    
    },
    
    {}
    
    ]}


خروجی مورد نیاز در  **USSD** : 

    [name] .1 , [id]
    
    [name].2 , [id]
    
    [name].3 , [id]
    
    [name].4 , [id]
    
    [name].5 , [id]

<div class="box-end">
</div>

## سرویس فعال کردن برداشت وجه خودکار صنف

خروجی خام یا جیسان سرویس :

    {
    
    "hasError": false,
    
    "referenceNumber":"360175",
    
    "errorCode":0,
    
    "count": 0,
    
    "ott": "d635b898b51feb3",
    
    "result": true
    
    }

خروجی مورد نیاز در  **USSD** : 

فعال سازی برداشت وجه خودکار صنف با موفقیت انجام شد.

    {
    
    "hasError": true,
    
    "referenceNumber": "360176",
    
    "errorCode":999,
    
    "message"این حساب شما در حال حاضر دارای تسویه حساب خودکار می باشد",
    
    "count": 0,
    
    "ott": "3080011c70c64715"
    
    }

خروجی مورد نیاز در  **USSD** : 

    [message]

<div class="box-end">
</div>

## غیر فعال کردن سرویس  برداشت وجه خودکار صنف

خروجی خام یا جیسان سرویس :

    {
    
    "hasError": false,
    
    "referenceNumber":"360175",
    
    "errorCode":0,
    
    "count": 0,
    
    "ott": "d635b898b51feb3",
    
    "result": true
    
    }

خروجی مورد نیاز در  **USSD** : 

غیر فعال کردن برداشت وجه خودکارصنف با موفقیت انجام شد.

    {
    
    "hasError": true,
    
    "referenceNumber": "360176",
    
    "errorCode":999,
    
    "message" درخواستتسویه حساب خودکار یافت نشد",",
    
    "count": 0,
    
    "ott": "3080011c70c64715"
    
    }

خروجی مورد نیاز در  **USSD** : 

    [message]

<div class="box-end">
</div>
