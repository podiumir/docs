- [مقدمه](#menu)
- [پیش از شروع](#menu)
- [استعلام قبض](#menu)

## مقدمه
با استفاده از سرویس استعلام قبض همراه اول میتوانید از میزان بدهی و اطلاعات پرداخت قبض تلفن همراه مطلع شوید.

## پیش از شروع

* URL فراخوانی سرویس ها: https://api.pod.ir/srv/sc/nzh/doServiceCall
* تمامی درخواست ها با متد POST ارسال می­شوند.
* Header درخواست:
پارامترهای زیر در Header تمام درخواست ها ثابت است:

|           پارامتر    |    توضیحات                                 |
|----------------------:|---------------------------------------------:|
|    \_token\_    |    API token دریافتی از پنل کسب و کاری    |
|    \_token_issuer\_    |    این پارامتر دارای مقدار ثابت "1" است.    |
|    Content-Type    |    application/x-www-form-urlencoded    |
|   Authorization    |     دریافتی از سرویس دریافت توکن    |

* بدنه درخواست:
پارامترهای زیر در بدنه تمام درخواست ها ثابت است:

|    پارامتر    |    توضیحات    |
|-------------------:|----------------------------------------------------------------:|
|    scProductId    |    شناسه سرویس در حال استفاده    |
|    scApiKey    |    API Key دریافتی برای سرویس مورد   نظر از پنل کسب و کاری     |  


* json Object ها در پارامتری به نام body  ارسال می­شوند.
* ساختار پاسخ دریافتی پس از فراخوانی سرویس به صورت زیر است که پاسخ دریافتی از endpoint  مورد نظر در پارامتر result قرار دارد.

```javascript
{
  "hasError": false/true,
  "messageId": 0,
  "referenceNumber": "",
  "errorCode": 0,
  "count": 0,
  "ott": "",
  "result": {
    "result": "response",
    "header": {},
    "statusCode":
  }
}
```
<div class="box-end">
</div>

## استعلام قبض


- شناسه سرویس : 49956
- پارامترهای ورودی : 

|توضیحات|پارامتر| 
|-------|-----------|
| شماره موبایل |mobileNumber |

- پاسخ‌های برگشتی


#### فراخوانی موفق

```javascript 

{

  "IsSuccess": "true",

  "ResultData": {

    "BillAmount":"میزان بدهی",

    "BillId": "شناسه قبض",

    "PaymentId": "شناسه پرداخت"

  },

  "Message": null,

  "SeqNumber": "0",

  "RefrenceNumber": "0",

  "Result": "Unknown"

}
```

#### شماره موبایل نامعتبر

```javascript 

{
  "IsSuccess": "false",

  "ResultData": "10",

  "Message": "شماره موبایل یافت نشد",

  "SeqNumber": "0",

  "RefrenceNumber": "0",

  "Result": "Unknown"

}
```

#### قبض پرداخت شده است:


```javascript 

{

  "IsSuccess": "false",

  "ResultData": "30",

  "Message": "تسویه شده است",

  "SeqNumber": "0",

  "RefrenceNumber": "0",

  "Result": "Unknown"

}

```
