- [مقدمه](#menu)
- [ عضویت و لغو عضویت مشتری در قرارداد](#menu)
- [ دریافت لیست طرح های قابل استفاده](#menu)
- [ تغییر طرح بازپرداخت تسهیلات](#menu)
- [ دریافت لیست تسهیلات](#menu)
- [ دریافت لیست اقساط](#menu)
- [درگاه پرداخت اقساطی](#menu)
- [ پرداخت فاکتور با استفاده از تسهیلات](#menu)

  
## مقدمه


##  عضویت و لغو عضویت مشتری در قرارداد
کسب و کار می‌تواند در هر قرارداد تسهیلات، مشتریان مورد تایید را عضو نموده و به ازای هر شخص استفاده کننده در قرارداد، سقف اعتبار تعیین نماید. جهت افزون مشتری به قرارداد، افزایش و یا کاهش سقف اعتبار تسهیلات به صورت گروهی، می‌توانید از طریق سرویس زیر اقدام نمایید. لازم به ذکر است کاربران دارای دسترسی، مجاز به استفاده ازاین سرویس می‌باشند.
  
  ```javascript 
 HEADER:
        _token_=[api_token]
        _token_issuer_= 1
        Content-Type=application/x-www-form-urlencoded
Method: POST
Url:
        [platform-address]/nzh/biz/updateLoanGrantorCreditForUsers
Parameters:
        fileId= *               //شناسه فایل حاوی اطلاعات افراد و مبلغ اعتبار        
        hashCode= *             //hashCode فایل آپلود شده
        contractId= *           //شناسه قرارداد
     
  ```
    
 سرویس فوق آدرس یک فایل را دریافت می‌نماید که میزان اعتبار هر کاربر در آن نشان داده .
شده است. جهت اطلاع از فرمت فایل ورودی، فایل پیوست را مشاهده نمایید:
  
  [نمونه فایل ورودی](https://core.pod.ir/nzh/file/?fileId=428089&hashCode=17288ac21a6-0.5468500634115298)

سرویس فوق، خروجی مشابه زیر برمی‌گرداند که شامل یک فایل است و با قرار دادن مقادیر fileId و hashCode در آدرس =file-address}}/nzh/file?fileId=&hashCode}} قابل دانلود می‌باشد.
```javascript 
{
  "hasError": false,
  "referenceNumber": "5101032",
  "errorCode": 0,
  "count": 0,
  "ott": "5e72a7828e383b15",
  "result": {
    "id": 13034,
    "name": "result-Sat Jun 06 10:24:33 UTC 2020.xlsx",
    "hashCode": "172892921ea-0.2993824288209098",
    "size": 0
  }
}
```
جهت حذف کاربران مجاز به استفاده از قرارداد تسهیلاتی از قرارداد، می‌توانید از سرویس زیر استفاده نمایید:

```javascript
HEADER:
        _token_=[api_token]
        _token_issuer_= 1
        Content-Type=application/x-www-form-urlencoded
Method: POST
Url:
        [platform-address]/nzh/biz/removePermittedUserFromLoanContract
Parameters:
        contractId= *               //شناسه قرارداد        
        userId=                     //شناسه کاربر                    
        cellphoneNumber=            //شماره موبایل تایید شده کاربر          
        nationalCode=               //کد ملی تایید شده کاربر
        username=                   //نام کاربری
```

## دریافت لیست طرح های قابل استفاده

برای هر قرارداد تسهیلات، با فراخوانی سرویس زیر می‌­توانید سایر طرح‌های قابل استفاده را دریافت نمایید:
```javascript
HEADER:
        _token_=[access_token]
        _token_issuer_= 1
Method: GET
Url:
        [platform-address]/nzh/loanPlanList
Parameters:
        id=
        name=              
        active=
        createDateFrom= 	
        createDateTo= 
        creator=
        grantorId= 
        contractId= 
        interestRate= 
        useable=
        offset= *
        size= *
    ```
   با فراخوانی سرویس فوق، خروجی مشابه زیر دریافت می‌گردد:
   ```javascript
  {
    "hasError": false,
    "referenceNumber": "5102111",
    "errorCode": 0,
    "count": 2,
    "ott": "189c557932e8da0c",
    "result": [
        {
            "id": 677,
            "name": "طرح بازپرداخت 6 ماهه با سود 6 درصد",
            "script": "...",
            "contract": {
                "id": 864,
                "guarantor": "LOAN_GUARANTOR_NO_GUARANTOR",
                "name": "ContractName",
                "uniqueId": "e749d4a694234f2dbb4cb1a10e149bc6",
                "grantor": {
                    "id": 164,
                    "business": {
                        "id": 1926,
                        "name": "لیلا",
                        "numOfProducts": 1872,
                        "rate": {
                            "rate": 0.0,
                            "rateCount": 0
                        },
                        "sheba": "290570021910012274315001",
                        "serviceCallName": "m1586934182886"
                    },
                    "supplyAmountTypeCode": "SUPPLY_LOAN_AMOUNT_TYPE_GUILD",
                    "supplyAmountValue": "BUSINESS_GUILD",
                    "enable": true,
                    "guild": {
                        "id": 44,
                        "name": "آرایش و زیبایی",
                        "code": "TOILETRIES_GUILD"
                    }
                },
                "creationDate": 1591441284373,
                "commissionRate": 2,
                "guaranteedRate": 300,
                "creator": {
                    "id": ...
                },
                "active": true,
                "versionNumber": "870-1",
                "lastVersion": true,
                "allBusinessesPermitted": true,
                "allProductsPermitted": true,
                "allContactTypesPermitted": true,
                "loanGrantorCeiling": 100000,
                "maxBreathingPeriodCount": 0,
                "endDate": 0
            },
            "creationDate": 1591441285369,
            "creator": {
                "id": ...
            },
            "active": true,
            "interestRate": 2,
            "penaltyScript": "..."
        },
        {
            "id": 676,
            "name": "طرح بازپرداخت یکساله با سود 12 در صد",
            "script": "...",
            "contract": {
                "id": 864,
                "guarantor": "LOAN_GUARANTOR_NO_GUARANTOR",
                "name": "ContractName",
                "uniqueId": "9675331c84e3469d9e428bef0c5f5823",
                "grantor": {
                    "id": 164,
                    "business": {
                        "id": 1926,
                        "name": "لیلا",
                        "numOfProducts": 1872,
                        "rate": {
                            "rate": 0.0,
                            "rateCount": 0
                        },
                        "sheba": "290570021910012274315001",
                        "serviceCallName": "m1586934182886"
                    },
                    "supplyAmountTypeCode": "SUPPLY_LOAN_AMOUNT_TYPE_GUILD",
                    "supplyAmountValue": "BUSINESS_GUILD",
                    "enable": true,
                    "guild": {
                        "id": 44,
                        "name": "آرایش و زیبایی",
                        "code": "TOILETRIES_GUILD"
                    }
                },
                "creationDate": 1591440614965,
                "commissionRate": 2,
                "guaranteedRate": 300,
                "creator": {
                    "id": ...
                },
                "active": true,
                "versionNumber": "869-1",
                "lastVersion": true,
                "allBusinessesPermitted": true,
                "allProductsPermitted": true,
                "allContactTypesPermitted": true,
                "loanGrantorCeiling": 100000,
                "maxBreathingPeriodCount": 0,
                "endDate": 0
            },
            "creationDate": 1591440616050,
            "creator": {
                "id": ...
            },
            "active": true,
            "interestRate": 2,
            "penaltyScript": "..."
        }
    ]
}
 
   ``` 

## تغییر طرح بازپرداخت تسهیلات

مشتری می­‌تواند از طریق پیامک ارسالی و یا توسط سرویس زیر، تا قبل از پرداخت قسط اول، طرح بازپرداخت تسهیلات ایجاد شده را تغییر دهد. با ارسال شماره تسهیلات و شماره طرح جدید به سرویس زیر، طرح جدید برای تسهیلات تعیین شده و اقساط منطبق با آن ایجاد می­‌گردد.
```javascript
Header:
        _token_=[access_token]
        _token_issuer_=1
        Content-Type=application/x-www-form-urlencoded
Method: POST
Url:
        [platform-address]/nzh/updateLoanByPlan
Parameters:
        loanId= *               //شناسه تسهیلات
        planId= *               //شناسه طرح
```

لازم به ذکر است تغییر طرح  بازپرداخت، تنها برای یک‌بار امکان‌پذیر می‌باشد.

## دریافت لیست تسهیلات

جهت دریافت لیست تسهیلات اقساطی از سرویس زیر استفاده نمایید:
```javascript
HEADER:
        _token_=[api_token]
        _token_issuer_= 1
Method: GET
Url:
        [platform-address]/nzh/biz/loanList
Parameters: 
        id=                             //شناسه تسهیلات
        subjectInvoiceId=               //شناسه فاکتور اصلی که با دریافت تسهیلات پرداخت شده است
        prePaidInvoiceId=               //شناسه فاکتور پیش‌پرداخت
        preSettlementInvoiceId=         //شناسه فاکتور تسویه زودتراز موعد
        planId=                         //شناسه طرح
        contractId=                     //شناسه قرارداد
        billNumber=                     //شماره قبض
        clearInstallmentTool=           //محل وصول اقساط 
        clearInstallmentToolCode=       //نوع محل وصول اقساط
        assuranceNumber=                //شماره وثیقه
        assuranceIdentifier=            //شناسه وثیقه
        guarantorCode=                  //کد نوع ضامن
        creationDateFrom=               //شروع تاریخ ایجاد تسهیلات به شمسی
        creationDateTo=                 //پایان تاریخ ایجاد تسهیلات به شمسی
        settledDateFrom=                //شروع تاریخ تسویه زودتر از موعد تسهیلات به شمسی
        settledDateTo=                  //پایان تاریخ تسویه زودتر از موعد تسهیلات به شمسی
        canceledDateFrom=               //شروع تاریخ لغو تسهیلات به شمسی
        canceledDateTo=                 //پایان تاریخ لغو تسهیلات به شمسی
        statusCode=                     //کد وضعیت تسهیلات
        installmentStatusCode=          //کد وضعیت قسط
        userId=                         //شناسه کاربر دارنده تسهیلات
        fromAmount=                     //شروع مبلغ کل تسهیلات
        toAmount=                       //پایان مبلغ کل تسهیلات
        createdOffline=true/false       //تسهیلات ایجاد شده به صورت آفلاین (بدون انتخاب از طریق درگاه) 
        offset= *                       //فاصله از مبدا        
        size= *                         //اندازه خروجی
```

  

**جدول مربوط به توضیحات مقادیر پارامترهای فوق**


| **نام پارامتر** | **شرح** |
|-----|-----|
|clearInstallmentToolCode|کد محل تسویه اقساط که می‌تواند یکی از مقادیر زیر باشد: **LOAN_CLEAR_INSTALLMENT_TOOL_WALLET** **LOAN_CLEAR_INSTALLMENT_TOOL_DIRECT_DEBIT**   **LOAN_CLEAR_INSTALLMENT_TOOL_BANK_ACCOUNT_NUMBER** |
|clearInstallmentTool|محل تسویه اقساط که بر اساس کد محل تسویه تعیین می‌شود.در صورتی که کد  **wallet**  باشد این پارامتر می‌تواند یکی از کیف پول‌های معتبر در پلتفرم پاد باشد. مانند  **PODLAND_WALLET**  یا  **DIGIPAY_WALLET** در صورتی که کد **deposit** باشد، مقدار این پارامتر یک حساب پاسارگادی می‌باشد.|
|guarantorCode|می‌تواند یکی از کدهای زیر باشد: <br> **LOAN_GUARANTOR_NO_GUARANTOR**  **LOAN_GUARANTOR_PASARGAD** <br> اولی یعنی بدون ضامن و دومی با ضمانت بانک پاسارگاد است|
|statusCode|وضعیت کلی تسهیلات را فیلتر می­‌کند. و می‌­تواند شامل انواع زیر باشد:                   											                 			        **LOAN_STATUS_CREATED**                                                                                                                                                                                                              **LOAN_STATUS_CANCELED**                                             **LOAN_STATUS_DONE**                         **LOAN_STATUS_WAITING_TO_CREATE**  (در مورد طرح‌هایی که به صورت آفلاین انتخاب می‌شوند، تا زمان پاسخ مشتری به پیامک یا انتخاب طرح بازپرداخت از طریق پنل، حداکثر به مدت یک روز تسهیلات در این وضعیت قرار می‌گیرد.) |            
|installmentStatusCode|در صورت وجود حتی یک قسط با این وضعیت، اطلاعات کامل تسهیلات و تمام اقساط آن برگردانده می‌شود.وضعیت اقساط می‌تواند یکی از کدهای زیر باشد: <br> **INSTALLMENT_STATUS_CANCELED  (لغو شده)**   **INSTALLMENT_STATUS_DONE  (پرداخت شده)**   **INSTALLMENT_STATUS_WAITING_FOR_BANK_SETTLEMENT  (منتظر تسویه بانکی)** <br>             **INSTALLMENT_STATUS_PRE_SETTLED  (تسویه زودتر از موعد)**  **INSTALLMENT_STATUS_CREATED  (ایجاد شده)**    **INSTALLMENT_STATUS_DELETED  (حذف شده)**
  
  
هم‌چنین مشتری می‌تواند از طریق سرویس ذیل، نسبت به دریافت لیست تسهیلات دریافت شده (خریدهای تسهیلاتی) خود اقدام نماید:

```javascript 
HEADER:
        _token_=[access_token]
        _token_issuer_= 1
Method: GET
Url:
        [platform-address]/nzh/loanList
Parameters: 
        id=                             //شناسه تسهیلات
        subjectInvoiceId=               //شناسه فاکتور اصلی که با دریافت تسهیلات پرداخت شده است
        prePaidInvoiceId=               //شناسه فاکتور پیش‌پرداخت
        preSettlementInvoiceId=         //شناسه فاکتور تسویه زودتراز موعد
        planId=                         //شناسه طرح
        contractId=                     //شناسه قرارداد
        billNumber=                     //شماره قبض
        clearInstallmentTool=           //محل وصول اقساط 
        clearInstallmentToolCode=       //نوع محل وصول اقساط
        assuranceNumber=                //شماره وثیقه
        assuranceIdentifier=            //شناسه وثیقه
        guarantorCode=                  //کد نوع ضامن
        creationDateFrom=               //شروع تاریخ ایجاد تسهیلات به شمسی
        creationDateTo=                 //پایان تاریخ ایجاد تسهیلات به شمسی
        settledDateFrom=                //شروع تاریخ تسویه زودتر از موعد تسهیلات به شمسی
        settledDateTo=                  //پایان تاریخ تسویه زودتر از موعد تسهیلات به شمسی
        canceledDateFrom=               //شروع تاریخ لغو تسهیلات به شمسی
        canceledDateTo=                 //پایان تاریخ لغو تسهیلات به شمسی
        statusCode=                     //کد وضعیت تسهیلات
        installmentStatusCode=          //کد وضعیت قسط
        businessId=                     //شناسه کسب و کار ایجاد کننده تسهیلات
        fromAmount=                     //شروع مبلغ کل تسهیلات
        toAmount=                       //پایان مبلغ کل تسهیلات
        createdOffline=true/false       //تسهیلات ایجاد شده به صورت آفلاین (بدون انتخاب از طریق درگاه) 
        offset= *                       //فاصله از مبدا        
        size= *                         //اندازه خروجی
```

پس از فراخوانی سرویس لیست تسهیلات، خروجی مشابه زیر دریافت می‌گردد:
```javascript 
{
  "hasError": false,
  "referenceNumber": "5102321",
  "errorCode": 0,
  "count": 7,
  "ott": "cba8399ab78bb4b8",
  "result": [
    {
      "id": 1663,
      "creationDate": 1591074250308,
      "primaryAmount": 0,
      "installments": [
        {
          "id": 5511,
          "amount": 1043,
          "remainAmount": 1043,
          "dueDate": 1599004800000,
          "installmentId": 1,
          "status": "INSTALLMENT_STATUS_CREATED"
        },
        {
          "id": 5512,
          "amount": 1043,
          "remainAmount": 1043,
          "dueDate": 1601510400000,
          "installmentId": 2,
          "status": "INSTALLMENT_STATUS_CREATED"
        },
        {
          "id": 5513,
          "amount": 1043,
          "remainAmount": 1043,
          "dueDate": 1604102400000,
          "installmentId": 3,
          "status": "INSTALLMENT_STATUS_CREATED"
        },
        {
          "id": 5514,
          "amount": 1043,
          "remainAmount": 1043,
          "dueDate": 1606694400000,
          "installmentId": 4,
          "status": "INSTALLMENT_STATUS_CREATED"
        },
        {
          "id": 5515,
          "amount": 1043,
          "remainAmount": 1043,
          "dueDate": 1609286400000,
          "installmentId": 5,
          "status": "INSTALLMENT_STATUS_CREATED"
        },
        {
          "id": 5516,
          "amount": 1048,
          "remainAmount": 1048,
          "dueDate": 1611878400000,
          "installmentId": 6,
          "status": "INSTALLMENT_STATUS_CREATED"
        }
      ],
      "preSettlements": [
        {
          "id": 5711,
          "paidInstallmentCount": 0,
          "amount": 7085,
          "preSettlementId": 1
        },
        {
          "id": 5712,
          "paidInstallmentCount": 1,
          "amount": 6042,
          "preSettlementId": 2
        },
        {
          "id": 5713,
          "paidInstallmentCount": 2,
          "amount": 4999,
          "preSettlementId": 3
        },
        {
          "id": 5714,
          "paidInstallmentCount": 3,
          "amount": 3956,
          "preSettlementId": 4
        },
        {
          "id": 5715,
          "paidInstallmentCount": 4,
          "amount": 2913,
          "preSettlementId": 5
        },
        {
          "id": 5716,
          "paidInstallmentCount": 5,
          "amount": 1870,
          "preSettlementId": 6
        }
      ],
      "totalAmount": 7085,
      "uniqueNumber": "loan-1663",
      "statusCode": "LOAN_STATUS_CREATED",
      "business": {
        "id": 123,
        "name": "کسب و کار تست",
        "numOfProducts": 80,
        "rate": {
          "rate": 10,
          "rateCount": 1
        },
        "sheba": "360570028380000840539101"
      },
      "user": {
        "id": 621,
        "name": "نام و نام‌خانوادگی",
        "ssoId": "581",
        "ssoIssuerCode": 1
      },
      "active": true,
      "billNumber": "1",
      "persianCreationDate": "1399/03/13",
      "subjectInvoice": {
        "id": 40190,
        "totalAmountWithoutDiscount": 6500,
        "delegationAmount": 0,
        "totalAmount": 6500,
        "payableAmount": 7085,
        "vat": 585,
        "issuanceDate": 1587906954186,
        "deliveryDate": 0,
        "billNumber": "15",
        "paymentBillNumber": "1044985",
        "uniqueNumber": "5af37e3960af61e3",
        "paymentDate": 1591074250353,
        "payed": true,
        "serial": 0,
        "canceled": false,
        "cancelDate": 0,
        "business": {
          "id": 123,
          "name": "کسب و کار تست",
          "numOfProducts": 80,
          "rate": {
            "rate": 10,
            "rateCount": 1
          },
          "sheba": "360570028380000840539101"
        },
        "invoiceItemSrvs": [
          {
            "id": 40501,
            "productShortSrv": {
              "id": 19857,
              "name": "تست",
              "description": "تست",
              "price": 13,
              "attributeValues": [
                {
                  "code": "provider",
                  "name": "تامین کننده",
                  "value": "service_call"
                },
                {
                  "code": "guildcode",
                  "name": "صنف",
                  "value": "BUILDING_GUILD"
                },
                {
                  "code": "methodtype",
                  "name": "نوع متد",
                  "value": "get"
                }
              ],
              "templateCode": "service_call"
            },
            "amount": 6500,
            "description": "تست لیست",
            "quantity": 1,
            "discount": 0,
            "voucherUsageSrvs": []
          }
        ],
        "guildSrv": {
          "id": 45,
          "name": "بهداشت و درمان",
          "code": "HEALTH_GUILD"
        },
        "userSrv": {
          "id": 621,
          "name": "نام و نام‌خانوادگی",
          "ssoId": "581",
          "ssoIssuerCode": 1
        },
        "phoneNumber": "09301111111",
        "cellphoneNumber": "09301111111",
        "closed": false,
        "verificationNeeded": false,
        "wallet": "PODLAND_WALLET",
        "safe": false,
        "postVoucherEnabled": false,
        "referenceNumber": "4641698",
        "issuerSrv": {
          "id": 43,
          "name": "نام",
          "ssoId": "23",
          "ssoIssuerCode": 1,
          "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=11886&width=512&height=512&hashCode=16fc80e81cb-0.3805531307941309"
        },
        "willBeBlocked": false,
        "willBePaid": false,
        "unsafeCloseTimeOut": 0,
        "paymentToolCode": "PAYMENT_TOOL_ONLINE_CREDIT",
        "withdrawable": false,
        "shaparakTransactionDate": 0,
        "payer": {
          "id": 43,
          "name": "نام ",
          "ssoId": "23",
          "ssoIssuerCode": 1,
          "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=11886&width=512&height=512&hashCode=16fc80e81cb-0.3805531307941309"
        },
        "edited": false,
        "waiting": false,
        "subInvoice": false
      },
      "plan": {
        "id": 614,
        "name": "تست تسهیلات ",
        "creationDate": 1591014243616,
        "creator": {
          "id": 43,
          "name": "نام ",
          "ssoId": "23",
          "ssoIssuerCode": 1,
          "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=11886&width=512&height=512&hashCode=16fc80e81cb-0.3805531307941309"
        },
        "active": true,
        "interestRate": 4
      },
      "contract": {
        "id": 838,
        "guarantor": "LOAN_GUARANTOR_PASARGAD",
        "name": "تست تسهیلات",
        "grantor": {
          "id": 22,
          "business": {
            "id": 5021,
            "name": "تستی5",
            "numOfProducts": 7,
            "rate": {
              "rate": 0,
              "rateCount": 0
            },
            "sheba": "580170000000208861342001"
          },
          "supplyAmountTypeCode": "SUPPLY_LOAN_AMOUNT_TYPE_WALLET",
          "supplyAmountValue": "PODLAND_WALLET",
          "enable": true
        },
        "loanGrantorCeiling": 0,
        "creationDate": 1591013756285,
        "endDate": 1616099400000,
        "active": true,
        "versionNumber": "838-1"
      },
      "assuranceNumber": "100",
      "assuranceIdentifier": "5af37e3960af61e3",
      "clearInstallmentToolId": "PODLAND_WALLET",
      "clearInstallmentToolCode": "LOAN_CLEAR_INSTALLMENT_TOOL_WALLET",
      "settledDate": 0,
      "canceledDate": 0,
      "breathingPeriodType": "LOAN_PLAN_BREATHING_PERIOD_TYPE_MONTHLY",
      "breathingPeriodCount": 3,
      "createdOffline": false
    }
  ]
}
```


## دریافت لیست اقساط

جهت دریافت وضعیت اقساط و لیست آن‌ها، سرویس زیر را فراخوانی نمایید:
```javascript
HEADER:
        _token_=[api_token]
        _token_issuer_= 1
Method: GET
Url:
        [platform-address]/nzh/biz/getInstallmentList
Parameters: 
        loanId= *                //شناسه تسهیلات
        id=                      //شناسه قسط
        invoiceId=               //فاکتور مربوط به پرداخت قسط
        fromDate=                //تاریخ شمسی
        toDate=                  //تاریخ شمسی
        statusCode=              //کد وضعیت قسط
        offset= *                //فاصله از مبدا        
        size= *                  //اندازه خروجی
```


در جدول زیر، تمامی حالت‌های موجود برای وضعیت قسط به همراه شرح آن آورده شده است:
  
  
| شرح | معادل فارسی | وضعیت قسط |
|----------|-----|------|
|قسط ایجاد شده ولی هنوز پرداخت نشده است.به محض سر رسید و داشتن موجودی در حساب کاربر، پرداخت خواهد شد. | ایجاد شده | INSTALLMENT_STATUS_CREATED |
| این قسط حذف شده است. | حذف شده | INSTALLMENT_STATUS_DELETED |
| این سفارش به علت عدم تایید فروشگاه در بازه زمانی مشخص، برگشت خورده است و اقساط آن لغو شده اند. | کنسل شده|  INSTALLMENT_STATUS_CANCELED |
| این قسط به موقع هنگام سررسید، پرداخت شده است. | پرداخت شده | INSTALLMENT_STATUS_DONE |
|تلاش برای پرداخت این قسط از سمت بانک به دلیل کسر موجودی مشتری، ناموفق بوده است. این قسط می‌بایست توسط کاربر شعبه و از حساب ضمانت مشتری پرداخت گردد.| منتظر تسویه بانکی |  INSTALLMENT_STATUS_WAITING_FOR_BANK_SETTLEMENT | 
| کاربر بر اساس الگوی تسویه زودتر از موعد ارسالی فروشگاه اقدام به تسویه زودتر از موعد نموده است و اقساط باقی‌مانده فاکتور را تسویه کرده است. | تسویه زودتر از موعد | INSTALLMENT_STATUS_PRE_SETTLED |



با فراخوانی سرویس فوق، خروجی مشابه زیر دریافت می‌گردد:
```javascript
{
  "hasError": false,
  "referenceNumber": "5120645",
  "errorCode": 0,
  "count": 6,
  "ott": "db4ae0ad8659a47b",
  "result": [
    {
      "id": 5392,
      "amount": 110,
      "remainAmount": 0,
      "dueDate": 1590969600000,
      "installmentId": 1,
      "status": "INSTALLMENT_STATUS_DONE",
      "relatedInvoices": [
        {
          "id": 44121,
          "totalAmountWithoutDiscount": 97,
          "delegationAmount": 0,
          "totalAmount": 97,
          "payableAmount": 97,
          "vat": 0,
          "issuanceDate": 1591140609856,
          "deliveryDate": 0,
          "billNumber": "a0d8e2eeaca6c499-1-615a3325-b620-4305-9ce0-a25a92612b7c",
          "paymentBillNumber": "1047688",
          "uniqueNumber": "c15a707c3985577",
          "description": "بابت پرداخت قسط شماره 1 تسهیلات شماره 1640",
          "paymentDate": 1591140609904,
          "payed": true,
          "serial": 0,
          "canceled": false,
          "cancelDate": 0,
          "business": {
            "id": 1806,
            "name": "نام",
            "numOfProducts": 7,
            "rate": {
              "rate": 0,
              "rateCount": 0
            },
            "sheba": "580170000000208861342001"
          },
          "invoiceItemSrvs": [
            {
              "id": 44613,
              "amount": 97,
              "description": "بابت پرداخت قسط شماره 1 تسهیلات شماره 1640",
              "quantity": 1,
              "discount": 0,
              "voucherUsageSrvs": []
            }
          ],
          "guildSrv": {
            "id": 45,
            "name": "بهداشت و درمان",
            "code": "HEALTH_GUILD"
          },
          "userSrv": {
            "id": 2868,
            "name": "نام",
            "ssoId": "6967",
            "ssoIssuerCode": 1,
            "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=7682&width=280&height=280&hashCode=16a81d60589-0.7772741446266116"
          },
          "phoneNumber": "02155555555",
          "cellphoneNumber": "09101234567",
          "closed": true,
          "verificationNeeded": false,
          "wallet": "PODLAND_WALLET",
          "customerInvoice": {
            "id": 44120,
            "totalAmountWithoutDiscount": 110,
            "delegationAmount": 0,
            "totalAmount": 110,
            "payableAmount": 110,
            "vat": 0,
            "issuanceDate": 1591140609853,
            "deliveryDate": 0,
            "paymentBillNumber": "1047688",
            "uniqueNumber": "d273acda6dcad1bd",
            "description": "بابت پرداخت قسط شماره 1 تسهیلات شماره 1640",
            "paymentDate": 1591140609927,
            "payed": true,
            "serial": 0,
            "canceled": false,
            "cancelDate": 0,
            "business": {
              "id": 1806,
              "name": "نام",
              "numOfProducts": 7,
              "rate": {
                "rate": 0,
                "rateCount": 0
              },
              "sheba": "580170000000208861342001"
            },
            "invoiceItemSrvs": [
              {
                "id": 44612,
                "amount": 110,
                "description": "بابت پرداخت قسط شماره 1 تسهیلات شماره 1640",
                "quantity": 1,
                "discount": 0,
                "voucherUsageSrvs": []
              }
            ],
            "guildSrv": {
              "id": 45,
              "name": "بهداشت و درمان",
              "code": "HEALTH_GUILD"
            },
            "userSrv": {
              "id": 2868,
              "name": "نام ",
              "ssoId": "6967",
              "ssoIssuerCode": 1,
              "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=7682&width=280&height=280&hashCode=16a81d60589-0.7772741446266116"
            },
            "phoneNumber": "02155555555",
            "cellphoneNumber": "09101234567",
            "closed": true,
            "verificationNeeded": false,
            "wallet": "PODLAND_WALLET",
            "safe": false,
            "postVoucherEnabled": false,
            "issuerSrv": {
              "id": 2688,
              "name": "نام ",
              "ssoId": "6788",
              "ssoIssuerCode": 1
            },
            "willBeBlocked": false,
            "willBePaid": false,
            "unsafeCloseTimeOut": 0,
            "paymentToolCode": "PAYMENT_TOOL_CREDIT",
            "withdrawable": true,
            "shaparakTransactionDate": 0,
            "payer": {
              "id": 2868,
              "name": "نام ",
              "ssoId": "6967",
              "ssoIssuerCode": 1,
              "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=7682&width=280&height=280&hashCode=16a81d60589-0.7772741446266116"
            },
            "depositId": "9951435100120005/inv-4412097/258",
            "edited": false,
            "subInvoice": false,
            "waiting": false
          },
          "subInvoices": [
            {
              "id": 44122,
              "totalAmountWithoutDiscount": 13,
              "delegationAmount": 0,
              "totalAmount": 13,
              "payableAmount": 13,
              "vat": 0,
              "issuanceDate": 1591140609857,
              "deliveryDate": 0,
              "billNumber": "a0d8e2eeaca6c499-1-77e1a2cd-3608-46b9-a43b-0bf2606bf8c9",
              "paymentBillNumber": "1047688",
              "uniqueNumber": "cba765bc18721268",
              "description": "بابت پرداخت قسط شماره 1 تسهیلات شماره 1640",
              "paymentDate": 1591140609943,
              "payed": true,
              "serial": 0,
              "canceled": false,
              "cancelDate": 0,
              "business": {
                "id": 4316,
                "name": "نام کسب و کار",
                "numOfProducts": 0,
                "rate": {
                  "rate": 0,
                  "rateCount": 0
                },
                "sheba": "580170000000208861342001"
              },
              "invoiceItemSrvs": [
                {
                  "id": 44614,
                  "amount": 13,
                  "description": "بابت پرداخت قسط شماره 1 تسهیلات شماره 1640",
                  "quantity": 1,
                  "discount": 0,
                  "voucherUsageSrvs": []
                }
              ],
              "guildSrv": {
                "id": 48,
                "name": "اقتصاد و بازرگانی",
                "code": "BUSINESS_GUILD"
              },
              "userSrv": {
                "id": 2868,
                "name": "نام ",
                "ssoId": "6967",
                "ssoIssuerCode": 1,
                "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=7682&width=280&height=280&hashCode=16a81d60589-0.7772741446266116"
              },
              "phoneNumber": "02155555555",
              "cellphoneNumber": "09101234567",
              "closed": true,
              "verificationNeeded": false,
              "wallet": "PODLAND_WALLET",
              "safe": false,
              "postVoucherEnabled": false,
              "issuerSrv": {
                "id": 2688,
                "name": "shadi8381422 t8381422",
                "ssoId": "6788",
                "ssoIssuerCode": 1
              },
              "willBeBlocked": false,
              "willBePaid": false,
              "unsafeCloseTimeOut": 0,
              "paymentToolCode": "PAYMENT_TOOL_CREDIT",
              "withdrawable": true,
              "shaparakTransactionDate": 0,
              "payer": {
                "id": 2868,
                "name": "نام ",
                "ssoId": "6967",
                "ssoIssuerCode": 1,
                "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=7682&width=280&height=280&hashCode=16a81d60589-0.7772741446266116"
              },
              "edited": false,
              "subInvoice": true,
              "waiting": false
            }
          ],
          "safe": false,
          "postVoucherEnabled": false,
          "issuerSrv": {
            "id": 2688,
            "name": "نام ",
            "ssoId": "6788",
            "ssoIssuerCode": 1
          },
          "willBeBlocked": false,
          "willBePaid": false,
          "unsafeCloseTimeOut": 0,
          "paymentToolCode": "PAYMENT_TOOL_CREDIT",
          "withdrawable": true,
          "shaparakTransactionDate": 0,
          "payer": {
            "id": 2868,
            "name": "نام پرداخت‌کننده",
            "ssoId": "6967",
            "ssoIssuerCode": 1,
            "profileImage": "http://all-dev-fbp-frp-fnp.fns:8080/nzh/image/?imageId=7682&width=280&height=280&hashCode=16a81d60589-0.7772741446266116"
          },
          "edited": false,
          "subInvoice": false,
          "waiting": false
        }
      ],
      "penaltyList": []
    }
  ]
}
```

## درگاه پرداخت اقساطی
  
  درگاه پرداخت پاد، سایتی است متعلق به پاد که در آن خریدار پس از انتخاب موارد مورد خرید خود در سایت فروشنده، به آنجا هدایت می‌گردد. در نمودار زیر روند کلی فرآیند پرداخت اقساطی توسط مشتری، در درگاه پرداخت پاد نمایش داده شده است:
  ![](https://podspace.pod.ir/nzh/drive/downloadFile?hash=Q34VEAZWKV16TU7C)

  


  
  در صورتی که خریدار پس از انتخاب موارد خرید خود در سایت فروشنده، درگاه یکپارچه پاد را انتخاب نماید، صفحه‌ی ذیل نمایش داده می‌شود:
  ![](https://core.pod.ir/nzh/image/?imageId=431801&width=609&height=442&hashCode=172e56c472e-0.14816689094067537)
  
    
 همان‌طور که در تصویر فوق مشاهده می‌نمایید، به علت وجود قرارداد برای فروشنده، گزینه‌ی "پرداخت از طریق درگاه اقساطی" نمایش داده می‌شود. لازم به ذکر است، مشتری همواره می‌تواند به روش‌های عادی پرداخت، مانند درگاه شاپرکی یا کیف پول، پرداخت خود را انجام دهد.

در صورتی که بیش از یک قرارداد فعال برای مشتری وجود داشته باشد، مشتری می‌تواند با انتخاب یکی از طرح‌ها نسبت به خرید اقساطی اقدام نماید:

![](https://core.pod.ir/nzh/image/?imageId=431802&width=559&height=288&hashCode=172e56c4798-0.5918227712220072)



![](https://core.pod.ir/nzh/image/?imageId=431803&width=555&height=318&hashCode=172e56c47be-0.7190929232631217)



چنان‌چه ضامن قرارداد بانک پاسارگاد باشد، صفحه‌ی ورود به اینترنت بانک مشابه تصویر ذیل نمایش داده شده و مشتری بایستی با ورود اطلاعات صحیح، هویت خود را تایید نماید. مشتری جهت ورود به اینترنت بانک، بایستی نام کاربری و رمز عبور اینترنت بانک پاسارگاد خود را داشته باشد.

لازم به ذکر است جهت ضمانت توسط بانک پاسارگاد، مشتری بایستی برای تامین اعتبار لازم، به شعب بانک پاسارگاد مراجعه نموده و یک حساب خود را جهت خرید اقساطی وثیقه نماید.


![](https://core.pod.ir/nzh/image/?imageId=431815&width=564&height=606&hashCode=172e5aa1a5f-0.10160555709445185)


در صورت وجود قرارداد فعال بدون ضامن برای خریدار، مشتری بدون احراز هویت توسط ضامن وارد صفحه ذیل می‌گردد. خریدار لیست اقساط و لیست تسویه زودتر از موعد را مشاهده نموده و با انتخاب محل پرداخت اقساط و وارد کردن سریال وثیقه خود، جهت پرداخت پیش‌پرداخت از طریق کیف پول یا درگاه بانک پاسارگاد اقدام می‌نماید.

لازم به ذکر است، به تعداد و به مبلغ هر قسط، در موعد مقرر فاکتور جدید برای مشتری ثبت شده و فاکتورها از محل پرداخت اقساط، پرداخت می‌گردند.

![](https://core.pod.ir/nzh/image/?imageId=431816&width=618&height=361&hashCode=172e5b6b4ef-0.24155065399917164)


خریدار می‌تواند مبلغ پیش‌پرداخت را به میزان دلخواه افزایش دهد تا از تسهیلات کمتری استفاده نماید. به این ترتیب نسبت به مبلغ پیش پرداخت جدید، لیست اقساط به روز رسانی می‌گردد.

لازم به ذکر است، در صورت عدم پرداخت پیش پرداخت، تسهیلات فعال نمی‌گردد، مگر آنکه مبلغ پیش پرداخت برابر با صفر باشد. در این صورت نیز بایستی کاربر با انتخاب کیف پول، دریافت تسهیلات را تایید نماید.


![](https://core.pod.ir/nzh/image/?imageId=431817&width=804&height=765&hashCode=172e5b6b53b-0.09493227740134069)



#### همان‌طور که در تصویر فوق مشاهده می‌نمایید، محل پرداخت اقساط ‌می‌تواند یکی از موارد ذیل باشد:

- کیف پول پاد
- حساب بانک پاسارگاد
- Direct debit (مبالغ کم)


## پرداخت فاکتور با استفاده از تسهیلات

در صورتی که مشتری توسط کسب و کار صاحب قرارداد تایید گردیده و از طریق سرویس عضویت در قرارداد تسهیلات، عضو قرارداد شده باشد، می‌تواند با ارسال شناسه فاکتور و شناسه قرارداد در سرویس زیر، نسبت به پرداخت اقساطی فاکتور خود اقدام نماید به شرط آنکه فاکتور در شرایط قرارداد صدق نماید.

```javascript 
Header:
        _token_=[API_TOKEN]
        _token_issuer_=1
Method: GET
Url:
        [platform-address]/nzh/payInvoiceByLoan
Parameters:
        invoiceId= *                         //شناسه فاکتور
        contractId= *                        //شناسه قرارداد تسهیلاتی
        planId=                              //شناسه طرح فروش اقساطی
        primaryAmount=                       //مبلغ پیش پرداخت
        assuranceNumber=                     //شماره وثیقه
        breathingPeriodType=                 //کد نوع دوره تنفس طرح بازپرداخت
        breathingPeriodCount=                //تعداد دوره تنفس طرح بازپرداخت 
```

در صورت وارد نکردن مقدار پارامترهای breathingPeriodType و breathingPeriodCount، تاریخ سرررسید اقساط از همین امروزمحاسبه خواهد گردید.

