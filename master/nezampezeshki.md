- [مقدمه](#menu)
- [پیش از شروع](#menu)
- [دریافت کد شهرها](#menu)
- [دریافت شماره نظام پزشکی از روی کد ملی](#menu)
- [دریافت نام و نام خانوادگی پزشک از روی شماره نظام پزشکی](#menu)
- [دریافت مدرک تحصیلی پزشک، شهر، تاریخ فارغ التحصیلی از روی شماره نظام پزشکی](#menu)
- [دریافت آدرس مطب، کدپستی، از روی شماره نظام پزشکی](#menu)
- [دریافت تلفن مطب از روی شماره نظام پزشکی](#menu)
- [دریافت تاریخ صدور و انقضا پروانه و شهر مجاز طبابت از روی شماره نظام پزشکی](#menu)
- [دریافت شماره نظام پزشکی از روی شهرمجاز پروانه و مدرک تحصیلی](#menu)
- [دریافت کد نظام پزشکی از روی نام و نام خانوادگی پزشک](#menu)
- [دریافت اطلاعات کارت دیجیتال عضو از روی کد ملی](#menu)
- [دریافت آدرس مطب، استان،شهر،آدرس، از روی شماره نظام پزشکی](#menu)
 
 
 ## مقدمه
با استفاده از سرویس های سازمان نظام پزشکی میتوانید اطلاعات مختلف مربوط به یک پزشک را (نام، شماره نظام پزشکی، آدرس مطب و...) با توجه به ورودی های مختلف دریافت کنید.
<div class="box-end">
</div>

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

* بدنه درخواست:
پارامترهای زیر در بدنه تمام درخواست ها ثابت است:

|    پارامتر    |    توضیحات    |
|-------------------:|----------------------------------------------------------------:|
|    scProductId    |    شناسه سرویس در حال استفاده    |
|    scApiKey    |    API Key دریافتی برای سرویس مورد   نظر از پنل کسب و کاری     |  

- جهت دریافت apikey کالکشن postman زیر را دریافت کنید. ابتدا میبیاست سرویس **درخواست سرویس** را اجرا کنید وسپس پارامتر id بازگشتی در پاسخ این سرویس را در سرویس **دریافت apikey** وارد و apikey را دریافت کنید. این مقادیر در قسمت examples درخواست های postman مشخص شده اند.  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[کالکشن postman راهنمای دریافت apikey](https://space.pod.ir/file/B9SAPKV6CHX9MUX6?dl=1)

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

## دریافت کد شهرها


- شناسه سرویس : 51829
- پارامترهای ورودی : ندارد
- پاسخ برگشتی:

``` javascript
{
   {
    "Result": [
        {
            "Id": "d9d94d63-a615-4cf9-b8f0-00335d6f1aed",
            "Name": "محمدیه"
        },
        {
            "Id": "9f68b9df-99dc-44b9-a816-003fd1ec96eb",
            "Name": "Kaifeng"
        },…….]
  }
}
```

## دریافت لیست مدارک تحصیلی
* شناسه سرویس: 71277
* پارامترهای ورودی: ندارد
* پاسخ برگشتی:

```javascript
{
    "Result": [
        {"Id": شناسه رشته مقطع, 
       "Title":نام رشته مقطع},
...
    ],
    "Script": null,
    "Html": null,
    "IsSuccess": true,
    "Message": null,
    "Exception": null
} 

```

## دریافت شماره نظام پزشکی از روی کد ملی


- شناسه سرویس : 45682
- پارامترهای ورودی


|توضیحات|پارامتر|
|----|----|
|کد ملی پزشک|nationalCode|

- پاسخ برگشتی:

``` javascript
{
 "Result": [
   {
   "McCode": ""
   }
  ],
 "Script": null,
 "Html": null,
 "IsSuccess": true,
 "Message": null,
 "Exception": null
}
```

## دریافت نام و نام خانوادگی پزشک از روی شماره نظام پزشکی

- شناسه سرویس: 45685
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|شماره نظام‌پزشکی|mcCode|

- پاسخ برگشتی:

``` javascript


{
"Result": {
 "FirstName": "",
 "LastName": "",
 "FirstNameNS": "",
 "LastNameNS": ""
},
"Script": null,
"Html": null,
"IsSuccess": true,
"Message": null,
"Exception": null
}
```

## دریافت مدرک تحصیلی پزشک، شهر، تاریخ فارغ التحصیلی از روی شماره نظام پزشکی
- شناسه سرویس: 45690
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|شماره نظام‌پزشکی|mcCode|

- پاسخ برگشتی:

``` javascript

{
"Result": {
 "Spec_DegreeFieldTitle": "دکترای حرفه‌ای پزشکی",
 "Spec_DateShamsi": "13810116",
 "Spec_InstituteCityTitle": "کرمان"
},
"Script": null,
"Html": null,
"IsSuccess": true,
"Message": null,
"Exception": null
}
```

## دریافت آدرس مطب، کدپستی، از روی شماره نظام پزشکی
- شناسه سرویس: 45695
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|شماره نظام‌پزشکی|mcCode|

- پاسخ برگشتی:

```javascript
{
 "Result": [
   {
   "Office_PostalCode": "کد پستی"
   },...
 ],
 "Script": null,
 "Html": null,
 "IsSuccess": true,
 "Message": null,
 "Exception": null
}
```


## دریافت تلفن مطب از روی شماره نظام پزشکی
- شناسه سرویس: 45754
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|شماره نظام‌پزشکی|mcCode|

- پاسخ برگشتی:

``` javascript

{
 "Result":[
  {
  "Office_TelCode": "کد شهر",
  "Office_Tel": "شماره تلفن"
  },...
 ],
 "Script": null,
 "Html": null,
 "IsSuccess": true,
 "Message": null,
 "Exception": null
}

```

## دریافت تاریخ صدور و انقضا پروانه و شهر مجاز طبابت از روی شماره نظام پزشکی
- شناسه سرویس: 45755
- پارامترهای ورودی:


|توضیحات|پارامتر|
|----|----|
|شماره نظام‌پزشکی|mcCode|

- پاسخ برگشتی:

``` javascrpit
{
 "Result":[
  {
  "PM_StartDateShamsi": "تاریخ شروع اعتبار به شمسی",
  "PM_StartDate": "تاریخ شروع اعتبار میلادی",
  "PM_ExpireDateShamsi": "تاریخ اتمام اعتبار به شمسی",
  "PM_ExpireDate": "تاریخ اتمام اعتبار به میلادی",
  "PM_CityTitle" : "شهر مجاز پروانه"
  },...
 ],
 "Script": null,
 "Html": null,
 "IsSuccess": true,
 "Message": null,
 "Exception": null
}
```


## دریافت شماره نظام پزشکی از روی شهرمجاز پروانه و مدرک تحصیلی

- شناسه سرویس: 51838
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|کد‌ شهر|cityId|
|مدرک تحصیلی|degreeFiedId|
|شماره صفحه|pageNumber|
|تعداد رکورد در هر صفحه|pageSize|


- پاسخ برگشتی:

``` javascript 
{
 "Result":{
  "TotalSize":تعداد کل رکوردهایی که با جستجو مطابقت دارد,
  "PageSize":تعداد رکورد در هر صفحه ارسالی,
  "PageNumber":شماره صفحه ارسالی,
  "PageCount":تعداد کل صفحات,
  "Items":[
   "شماره نظام اول",
   "شماره نظام دوم",
   ...
  ]
 } ,
 "Script": null,
 "Html": null,
 "IsSuccess": true,
 "Message": null,
 "Exception": null
}
```


## دریافت کد نظام پزشکی از روی نام و نام خانوادگی پزشک

- شناسه سرویس: 51837
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|کد‌ شهر|firstName|
|مدرک تحصیلی|lastName|
|شماره صفحه|pageNumber|
|تعداد رکورد در هر صفحه|pageSize|


- پاسخ برگشتی:

``` javascript

{
 "Result":{
  "TotalSize":تعداد کل رکوردهایی که با جستجو مطابقت دارد,
  "PageSize":تعداد رکورد در هر صفحه ارسالی,
  "PageNumber":شماره صفحه ارسالی,
  "PageCount":تعداد کل صفحات,
  "Items":[
   "شماره نظام اول",
   "شماره نظام دوم",
   ...
  ]
 },
 "Script": null,
 "Html": null,
 "IsSuccess": true,
 "Message": null,
 "Exception": null
}
```

## دریافت اطلاعات کارت دیجیتال عضو از روی کد ملی 

- شناسه سرویس: 51831
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|کد ملی|nationalCode|

- پاسخ برگشتی:

``` javascript
{
 "Result": {
  "FirstName": "نام",
  "LastName": "نام خانوادگی",
  "DateOfCreation": "تاریخ صدور (تاریخ شمسی)",
  "ExpiryDate": "تاریخ پایان اعتبار (تاریخ شمسی)",
  "CardStatusTitle": "نام وضعیت کارت"
  "CardStatus": "وضعیت کارت صادر شده شامل کلاسی با مقادیر (فعالی=Issued / معلق=Suspended / باطل=Revoked)"
  "CardStatusID": "شناسه وضعیت کارت"
 },
 "Script": null,
 "Html": null,
 "IsSuccess" : true,
 "Message"  : null,
 "Exception" : null
}
```

## دریافت آدرس مطب، استان،شهر،آدرس، از روی شماره نظام پزشکی
- شناسه سرویس: 45673
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|کد ملی|nationalCode|

- پاسخ برگشتی:

``` javascript
{
"Result": [
 {
 "Office_ProvinceTitle": "استان",
 "Office_CityTitle": "شهر",
 "Office_Address": "آدرس",
 "AddressType" : "نوع آدرس"
 },...
],
"Script": null,
"Html": null,
"IsSuccess": true,
"Message": null,
"Exception": null
}
```
