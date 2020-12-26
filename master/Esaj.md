- [مقدمه](#menu)
- [پیش از شروع](#menu)
- [سرویس خرید شارژ مستقیم](#menu)
- [وضعیت نهایی سفارش](#menu)
- [استعلام بسته‌های اینترنتی](#menu)
- [استعلام دسته بندی­‌های بسته پیشنهادی ایرانسل](#menu)
- [استعلام  بسته‌های پیشنهادی ایرانسل](#menu)

## مقدمه
با استفاده از سرویسهای شارژ مستقیم ایساج میتوانید به راحتی برای هر شماره تلفن همراهی شارژ تهیه کنید.

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

## سرویس خرید شارژ مستقیم

- عملکرد: این سرویس  بر اساس اطلاعات ورودی مانند شماره موبایل، مبلغ شارژو ... خرید شارژ را انجام می­دهد و وضعیت پرداخت و پیغام مربوط به آن را به عنوان خروجی نمایش می­دهد.
- شناسه سرویس: 130134
- پارامترهای ورودی:

|توضیحات|پارامتر|
|----|----|
|شماره موبایل|MobileNumber|
|مبلغ شارژ|price|
|شماره محصول|product|
|شماره سفارش|order_id|
|نوع سفارش|Type|
|پروفایل آیدی بسته‌­های ایرانسل|profile_id|
|نوع بستر شارژ|ext_id|
|کد ملی|national_code|
|نام فروشگاه|store_name|

 برای مقدار پارامتر ورودی شماره محصول (product)، از جدول زیر می­توانید استفاده کنید:  
 
 |ورودی|محصول|
 |---|---|
 |2|رایتل|
 |4|همراه اول|
 |5|ایرانسل|

برای مقدار پارامتر ورودی نوع سفارش (type)، از جدول زیر می­توانید استفاده کنید:  

|ورودی|نوع شارژ|
|----|----|
|1|همراه اول|
|بسته اینترنتی همراه اول|6|
|2|شارژ معمولی رایتل|
|3|شارژ شورانگیز رایتل|
|7|بسته اینترنتی رایتل|
|2|ایرانسل شگفت انگیز|
|4|ایرانسل ثابت|
|5|بسته اینترنتی ایرانسل|
|8|بسته پیشنهادی|
|رشته خالی|وایمکس ایرانسل و ایرانسل معمولی|


فقط در صورتی نیاز به ارسال پارامتر profile_id می­باشد که شارژ مستقیم درخواستی، نوع بسته اینترنتی و یا خرید بسته پیشنهادی ایرانسل باشد و در غیر این صورت نیازی به ارسال این پارامتر نیست.

- مبلغ شارژ (price) را بر اساس جدول زیر وارد نمایید:  


|ویژگی‌های قیمت|محصول|
|----|----|
|حداقل 10000 ریال و حداکثر 1000000 ریال و مضرب 1000 ریال|همراه اول|
|مبالغ زیر شامل:10000-20000-50000-10000-200000|ایرانسل شگفت‌انگیز|
|حداقل 5000 و حداکثر 1000000|ایرانسل وایمکس،معمولی و ثابت|
|اعلام شده توسط ایرانسل|ایرانسل بسته اینترنتی و بسته پیشنهادی|
|حداقل 10000 و حداکثر 1000000|رایتل معمولی|
|یکی از قیمت های زیر:20000- 50000-100000-200000-500000-1000000|رایتل شورانگیز|

- مقدار پارامتر ورودی نوع بستر شارژ (ext_id)  را بر اساس جدول زیر وارد نمایید:

|ورودی|نوع بستر شارژ|
|-----|-----|
|59|بستر اینترنت|
|15|بستر موبایل اپ|

#### نمونه پارامترهای ورودی:
```javascript
{
	MobileNumber= 
	price=10000
	product=5
	order_id=0
	type=
	ext_id=59
	national_code=
	store_name=Esaj
}
```

- پارامترهای خروجی: خروجی سرویس خرید شارژ مستقیم دارای دو بخش status و message می‌باشد.
 پارامتر خروجی status می‌تواند به صورت جدول زیر باشد:

|وضعیت|کد|
|----|----|
|موفقیت آمیز|1|
|ناموفق از طرف اپراتور|0|
|عدم ذخیره سفارش|-1|
|نیاز به افزایش سپرده|-2|
|غیر فعال بودن محصول مورد نظر|-3|
|کاربر نامعتبر|-4|
|اتفاق پیش بینی نشده|-5|

در قسمت پارامتر خروجی message، .پیغام وضعیت درخواست در صورت موفقیت و یا عدم موفقیت برگشت خواهد داده شد

#### نمونه پاسخ برگشتی:

```javascript
<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<SOAP-ENV:Envelope
    xmlns:SOAP-ENV=\"http://schemas.xmlsoap.org/soap/envelope/\"
    xmlns:ns1=\"http://ws.esaj.ir/api/topup?ws=1\"
    xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"
    xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"
    xmlns:SOAP-ENC=\"http://schemas.xmlsoap.org/soap/encoding/\" SOAP-ENV:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\">
    <SOAP-ENV:Body>
        <ns1:getTopupResponse>
            <return xsi:type=\"xsd:string\">{"status":1,"message":"شارژ مستقیم با موفقیت انجام شد.\"}</return>
        </ns1:getTopupResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>

````

## وضعیت نهایی سفارش

- عملکرد:   این  سرویس  با دریافت شماره سفارش مربوط به سرویس خرید شارژ، وضعیت سفارش را نمایش می­دهد.
- شناسه سرویس: 68274
- پارامترهای ورودی: شماره سفارش

|توضیحات|پارامتر ورودی|
|-----|-----|
|شماره سفارش|Order_id|

#### نمونه پارامتر ورودی:
Order_id =0

- پارامترهای خروجی: خروجی سرویس دارای دو بخش status و message می‌باشد.

پارامترهای خروجی status  می‌تواند به صورت جدول زیر باشد:

|وضعیت|کد|
|-----|----|
|موفقیت‌آمیز|1|
|سفارش ناموفق|0|
|کاربر نامعتبر|-4|

در قسمت پارامتر خروجی message، پیغام وضعیت درخواست در صورت موفقیت و یا عدم موفقیت برگشت خواهد داده شد.

#### نمونه پاسخ برگشتی:

```javascript

<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<SOAP-ENV:Envelope
    xmlns:SOAP-ENV=\"http://schemas.xmlsoap.org/soap/envelope/\"
    xmlns:ns1=\"http://ws.esaj.ir/apiverify/verify?ws=1\"
    xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"
    xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"
    xmlns:SOAP-ENC=\"http://schemas.xmlsoap.org/soap/encoding/\" SOAP-ENV:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\">
    <SOAP-ENV:Body>
        <ns1:getVerifyResponse>
            <return xsi:type=\"xsd:string\">{\"شارژ مستقیم با موفقیت انجام شد.\: ":"status":1,"message"} </return>
        </ns1:getVerifyResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

## استعلام بسته‌های اینترنتی


- عملکرد:   این  سرویس  با دریافت شناسه مربوط به نوع اپراتور، بسته های اینترنتی موجود را نمایش می­دهد
- شناسه سرویس: 68277
- پارامترهای ورودی: شناسه اپراتور که در جدول product از سرویس شارژ مستقیم موجود است.

|توضیحات|پارامتر ورودی|
|----|----|
|شناسه اپراتور|Operator_id|

#### نمونه پارامتر ورودی:
Operator_id =5

- پارامترهای خروجی:

|توضیحات|پارامتر خروجی|
|-----|-----|
|نام بسته|name|
|قیمت بسته|price|
|پروفایل آی دی بسته|Profile_id|
|نام گروه بسته|category_name|
|نام گروه والد بسته|category_parent_name|
|شناسه بسته|category_id|
|شناسه والد بسته|category_parent_id|

#### نمونه پاسخ برگشتی:
```javascript

<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<SOAP-ENV:Envelope
    xmlns:SOAP-ENV=\"http://schemas.xmlsoap.org/soap/envelope/\"
    xmlns:ns1=\"http://ws.esaj.ir/apiinternet/packages?ws=1\"
    xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"
    xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"
    xmlns:SOAP-ENC=\"http://schemas.xmlsoap.org/soap/encoding/\" SOAP-ENV:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\">
    <SOAP-ENV:Body>
        <ns1:getPackagesResponse>
<return xsi:type=\"xsd:string\">[
  {
    “name”: “1/5 گیگابایت “,
    “price”: “80660”,
    “profile_id”: 61626,
    “category_name”: “روزانه”,
    “category_parent_name”: “بسته سیم کارت اعتباری”,
    “category_id”: 1,
    “category_parent_id”: 1
  },
  {
    “name”: “300 مگابایت”,
    “price”: “42510”,
    “profile_id”: 61623,
    “category_name”: “روزانه”,
    “category_parent_name”: “بسته سیم کارت اعتباری”,
    “category_id”: 1,
    “category_parent_id”: 1
  },
….
] </return>
</ns1:getPackagesResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>

```

## استعلام دسته بندی‌های بسته پیشنهادی ایرانسل

- عملکرد: این سرویس دسته بندی‌های پیشنهادی ایرانسل را ارائه می‌دهد.
- شناسه سرویس: 68287
- پارامترهای ورودی: پارامتر ورودی ندارد.
- پارامتر خروجی:

|توضیحات|پارامتر خروجی|
|----|----|
|بسته مکالمه ساعتی|Voice Hourly|
|بسته مکالمه روزانه|Voice Daily|
|بسته مکالمه هفتگی|Voice Weekly|
|بسته مکالمه ماهانه|Voice Monthly|
|بسته اینترنت ساعتی|Data Hourly|
|بسته اینترنت روزانه|Data Daily|
|بسته اینترنت هفتگی|Data Weekly|
|بسته اینترنت ماهانه|Data Monthly|

#### نمونه پاسخ برگشتی:

```javascript
<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<SOAP-ENV:Envelope
    xmlns:SOAP-ENV=\"http://schemas.xmlsoap.org/soap/envelope/\"
    xmlns:ns1=\"http://ws.esaj.ir/apioffercategory/categorypackages?ws=1\"
    xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"
    xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"
    xmlns:SOAP-ENC=\"http://schemas.xmlsoap.org/soap/encoding/\" SOAP-ENV:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\">
    <SOAP-ENV:Body>
        <ns1:getCategorypackagesResponse>
            <return xsi:type=\"xsd:string\">{
  "Voice Hourly": "Voice Hourly",
  "Voice Daily": "Voice Daily",
  "Voice Weekly": "Voice Weekly",
  "Voice Monthly": "Voice Monthly",
  "Data Hourly": "Data Hourly",
  "Data Daily": "Data Daily",
  "Data Weekly": "Data Weekly",
  "Data Monthly": "Data Monthly"
}</return>
        </ns1:getCategorypackagesResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>


```

## استعلام بسته‌های پیشنهادی ایرانسل

- عملکرد:  این  سرویس  با دریافت شماره موبایل ایرانسل و یکی از  دسته­بندی­های برگشت داده شده از سرویس " استعلام دسته بندی های بسته های پیشنهادی ایرانسل"، مشخصات بسته­های پیشنهادی ایرانسل مانند نام بسته پیشنهادی، شناسه پروفایل بسته و قیمت بسته را ارائه می­دهد
- شناسه سرویس: 68297
- پارامترهای ورودی: شماره موبایل و دسته بندی بسته

|توضیحات|پارامتر|
|----|----|
|شماره موبایل|MobileNumber|
|یکی از  دسته­‌بندی‌­های برگشت داده شده از سرویس " استعلام دسته بندی­‌های بسته­‌های پیشنهادی ایرانسل"|Category|

#### نمونه پارامتر ورودی: 

MobileNumber:

Category: Data Daily

- پارامتر خروجی:

|توضیحات|پارامتر خروجی|
|-----|-----|
|نام بسته|name|
|قیمت بسته|price|
|پروفایل آی دی بسته|Profile_id|

#### نمونه پاسخ برگشتی:

```javascript
<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<SOAP-ENV:Envelope
    xmlns:SOAP-ENV=\"http://schemas.xmlsoap.org/soap/envelope/\"
    xmlns:ns1=\"http://ws.esaj.ir/apioffer/packages?ws=1\"
    xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"
    xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\"
    xmlns:SOAP-ENC=\"http://schemas.xmlsoap.org/soap/encoding/\" SOAP-ENV:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\">
    <SOAP-ENV:Body>
        <ns1:getPackagesResponse>
            <return xsi:type=\"xsd:string\">
                {
  "0-41452": {
    "name": "1.5گیگ 4450ت",
    "profile_id": "0-41452",
    "price": "44500"
  },
  "0-41455": {
    "name": "1.5گیگ 4950ت",
    "profile_id": "0-41455",
    "price": "49500"
  }
}
            </return>
        </ns1:getPackagesResponse>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>



```


برای خرید بسته پیشنهادی باید profile_id، شماره موبایل و مبلغ شارژ را به سرویس خرید شارژ مستقیم باtype مشخص شده در جدول تایپ فرستاده تا شارژ انجام شود .نکته بسیار مهم، برای این مبلغ باید مبلغ­هایی که با سرویس استعلام بسته­های پیشنهادی برگشت داده می­شوند برای ارسال به سمت وب سرویس باید بعلاوه نه درصد  ارزش افزوده شود برای مثال مبلغ 5000 ریال باید 5450 به عنوان مبلغ به سرویس شارژ مستقیم ارسال شود.

