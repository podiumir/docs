- [مقدمه](#menu)
- [پیش از شروع](#menu)
- [دریافت فهرست اولیه هتل‌ها](#menu)
- [دریافت اطلاعات شهرها](#menu)
- [دریافت امکانات](#menu)
- [روش‌های پرداخت](#menu)
- [موجودی هتل](#menu)
- [دریافت اطلاعات قیمت و موجودی هتل](#menu)
- [موجودی هتل‌ها](#menu)
- [ثبت اولیه رزرو همگام](#menu)
- [ثبت رزرو ناهمگام](#menu)
- [تایید رزرو همگام](#menu)
- [تایید رزرو ناهمگام](#menu)
- [بررسی رزرو](#menu)
- [لغو رزرو](#menu)


## مقدمه
از مهم‌ترین نیازمندی‌ها برای رشد صنعت گردشگری، مناسب بودن خدمات اقامتی است. مسافران باید بتوانند از طریق آژانس‌های مسافرتی یا به طور مستقیم، اقامت‌گاه مناسب سفر خود را تهیه کنند. در شرایط کنونی رشد فناوری اطلاعات، این امر بیش از پیش اهمیت یافته‌­است. در دسترس­‌داشتن اطلاعات برای رزرو اقامت‌گاه‌ها برگ برنده هر آژانس گردشگری است. از طرفی، اقامت‌گاه‌ها نیز اگر نتوانند اطلاعات موجودی اتاق‌های خود را در دسترس مشتریان گسترده‌تری قرار دهند، نرخ اشغال اتاق‌هایشان کاهش خواهد یافت.

ارائه خدمتی که این دوسوی صنعت گردشگری را به یکدیگر متصل کند، ارزش افزوده مناسبی ایجاد خوهد کرد. امروزه، شرکت‌های مختلفی در سطح بین‌المللی این خدمات را ارائه می‌دهند. همزمان، شرکت‌های کوچکتری نیز در هر کشور شکل گرفته‌اند که زنجیره این خدمات را طولانی‌تر کرده و دسترسی آژانس‌ها و هتل‌های داخلی را به شبکه‌های بین‌المللی تسهیل می‌کنند.

شرکت لاماسو، با هدف ایجاد خدمتی که مشابه داخلی نداشته و با دیدگاهی که قابلیت توسعه کسب‌وکار را تضمین کند، به این عرصه وارد شده‌است و در نظر دارد از یک‌سو، تمام هتل‌های داخلی را به هسته مرکزی خود متصل کند و از سوی دیگر، با ارائه سرویس به آژانس‌های مسافرتی، به ایشان این امکان را بدهد تا با دسترسی به این حجم وسیع از هتل‌ها، خدمات مطلوبی را به گردشگران ارائه دهند.

راهکار لاماسو، استفاده از راهکارهای ارتباطی تمام برخط است که در فضای گردشگری فعلی کشور، نیاز مبرمی بدان حس می‌شود. با استفاده از این راهکار، استفاده نیروی انسانی به حداقل رسیده که سبب افزایش دقت و سرعت، با کاهش بارکاری نیروی انسانی می‌شود. براین اساس، طرح‌ریزی لاماسو از سال 1395 آغاز گردید. از آن زمان تا به‌حال، لاماسو با توسعه زیرساخت مناسب ارتباط اقامت‌گاه و مراکز فروش و با گسترش فعالیت‌های خود، راهکارهای مختلفی به‌منظور بهبود رویه‌های ارتباطی در صنعت گردشگری ارائه داده‌است.


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


## دریافت فهرست اولیه هتل­ها

با استفاده از این سرویس میتوانید لیست تمام هتل­های موجود و جزییات مربوط به آنها را دریافت کنید. این لیست فرکانس تغییر زیادی ندارد و نیاز به فراخوانی آن بیش از چند بار در روز نیست.

- شناسه سرویس: 51730
- پارامترهای ورودی:

|توضیحات|اختیاری|نوع|پارامتر|
|---|----|----|---|
|شناسه شهری که هتل­ها در آن هستند. اگر این مقدار ارسال نشود لیست تمامی هتل­ها در پاسخ بازگردانده خواهد شد.|*|string|city_id|

- پاسخ برگشتی:json با ساختار و پارامترهای زیر :

|توضیحات|نوع|پارامتر|
|---|----|----|
|زبان پاسخ برگشتی|string|lang|
| آرایه­ای از لیست object های شامل اطلاعات هتل­ها. این لیست فهرست کامل هتل­ها است. هر هتلی که در این لیست وجود نداشته باشد می­بایست از سایت کاربر حذف شود.|object[]|hotels|
|شناسه منحصربفردهتل.این شناسه ثابت خواهد بود و ماکزیمم دارای 30 کاراکتراشت|string|id|
|اگر هتل برای رزرو در دسترس باشد مقدار true و در غیر اینصورت false است.|boolean|available_for_booking|
| نام هتل. ماکزیمم دارای 300 کاراکتر است.|string|name|
|مشخص کننده نوع و درجه هتل بر اساس جدول 1|number|star|
|کد پستی هتل. ماکزیمم 20 کاراکتر.|string|postal_code|
|آدرس خیابان. ماکزیمم 300 کاراکتر|string|street|
|شناسه شهری که هتل در ان واقع است. ماکزیمم 30 کاراکتر|string|city|
|استان، ایالت یا محل­های جغرافیایی میان­رده هتل. ماکزیمم 100 کاراکتر|string|province|
|کشوری که هتل در ان واقع است. ماکزیمم 100 کاراکتر|string|province|
|طول جغرافیایی هتل|number|latitude|
|عرض جغرافیایی هتل|number|longitude|
|توضیحات هتل. ماکزیمم 1000 کاراکتر|string|desc|
|آرایه­ای از شناسه­های امکانات هتل، هر شناسه به یک سطح از امکانات هتل اشاره دارد. این امکانات مربوط به یک اتاق خاص نیست و کل هتل را شامل میشود.|string[]| amenities|
|آدرس ایمیل هتل. ماکزیمم 256 کاراکتر.|string|email|
|شماره تلفن هتل. ماکزیمم 50 کاراکتر|string|number|
|شماره فکس هتل. ماکزیمم 50 کاراکتر|string|fax|
|Object ای که انواع اتاق در هتل را توصیف میکند.|Object[]|Room_types|
|شناسه نوع اتاق|number|id|
|عنوان نوع اتاق. ماکزیمم 100 کاراکتر|string|title|
|توضیح مختصری از نوع اتاق. ماکزیمم 300 کاراکتر|string|desc|
|شناسه­ های امکانات هتل|string|amenities|
|ماکزیمم تعداد مهمانان مجاز در اتاق|number|capacity|
|ماکزیمم تعداد مهمانان مجاز اضافی در اتاق|number|extera_capacity|
|آرایه ه­ای از طبقه­ بندی و تعداد تخت­های موجود در یک اتاق|Object|bed_configurations|
|کد تخت OpenTravel|number|code|
|تعداد تخت­های از این نوع خاص در اتاق|number|count|
||BedConfiguration[]|extra_bed_configurations|
|کد تخت OpenTravel|number|code|
|تعداد تخت­های از این نوع خاص در اتاق|number|count|
|سیاست استعمال سیگار در هتل. یکی از مقادیر smoking یا non_smoking|string|smoking_policy|
|آرایه­‌ای از تصاویر اتاق|Object[]|images|
|آدرس url تصویر|string|url|
||string|caption|
|آرایه‌­ای از تصاویر هتل|Object[]|images|
|آدرس url تصویر|string|url|
||string|caption|
|آرایه‌ای از شناسه­ های سیاست­های مد نظر که هر شناسه به یک هتل مربوط میشود.|String[]|policies|


##### نمونه پاسخ برگشتی:


``` javascript 
{
  "api_version": "0.1.1",
  "lang": "fa_IR",
  "hotels": [
    {
      "id": 258705,
      "name": "هتل زیبا",
      "available_for_booking": "true",
      "star": 1,
      "street": "نام خیابان",
      "city": "eb34",
      "postal_code": "02215",
      "province": "تهران",
      "country": "ایران",
      "latitude": 42.348808,
      "longitude": -71.094971,
      "desc": "",
      "amenities": [],
      "email": "ziba@example.com",
      "phone": "+98212323232",
      "fax": "+98212323232",
      "room_types": [
        {
          "id": 1,
          "title": "اتاق دو تخته",
          "desc": "",
          "amenities": [],
          "capacity": 2,
          "extra_capacity": 0,
          "bed_configurations": [],
          "extra_bed_configurations": [],
          "smoking_policy": "",
          "images": []
        },
        {
          "id": 2,
          "title": "اتاق سه تخته",
          "desc": "",
          "amenities": [],
          "capacity": 3,
          "extra_capacity": 0,
          "bed_configurations": [],
          "extra_bed_configurations": [],
          "smoking_policy": "",
          "images": []
        },
        {
          "id": 3,
          "title": "اتاق چهار تخته",
          "desc": "",
          "amenities": [],
          "capacity": 4,
          "extra_capacity": 0,
          "bed_configurations": [],
          "extra_bed_configurations": [],
          "smoking_policy": "",
          "images": []
        },
        {
          "id": 4,
          "title": "سوییت",
          "desc": "",
          "amenities": [],
          "capacity": 4,
          "extra_capacity": 0,
          "bed_configurations": [],
          "extra_bed_configurations": [],
          "smoking_policy": "",
          "images": []
        }
      ],
      "images": [
        {
          "url": "http://example.com/img/1.jpg",
          "caption": ""
        }
      ]
    }
  ]
}
```

## دریافت اطلاعات شهرها


- شناسه سرویس: 51756
- پارامترهای ورودی: ندارد
- پاسخ برگشتی:json با ساختار و پارامترهای زیر :


|توضیحات|نوع|پارامتر|
|---|----|----|
|ورژن APIای که استفاده می‌شود|String|Api version|
|زبان پاسخ برگشتی|String|Lang|
|آرایه­‌ای از تمام شهرهایی که پشتیبانی می‌شود|Object[]|Cities|
|شناسه منحصربفردی که برای تشخیص شهر مورد نظر استفاده میشود.این شناسه تغییرنخواهد کرد وماکزیمم 30 کاراکتر است.|String|Id|
|نام شهر. ماکزیمم 300 کاراکتر|String|Name|
|کد IATA شهر|String|Code|


  
  
#### نمونه پاسخ برگشتی:

```javascript
{
  "api_version": "0.1.1",
  "lang": "en_US",
  "cities": [
    {
      "id": "eb33",
      "name": "Shiraz",
      "code": "SYZ"
    },
    {
      "id": "eb34",
      "name": "Mashhad",
      "code": "MHD"
    }
  ]
}
```

## دریافت امکانات


از این سرویس برای دریافت جزییات امکانات استفاده می­شود.

- شناسه سرویس: 51762
- پارامترهای ورودی: ندارد
- پاسخ برگشتی:json با ساختار و پارامترهای زیر :

|توضیحات|نوع|پارامتر|
|---|----|----|
|ورژن APIای که استفاده می‌شود|String|Api version|
|زبان پاسخ برگشتی|String|Lang|
|آرایه­‌ای از تمام امکاناتی که پشتیبانی می‌شود|Object[]|Amenities|
|شناسه منحصربفردی که برای تشخیص امکانات مورد نظر استفاده میشود.این شناسه تغییرنخواهد کرد وماکزیمم 30 کاراکتر است.|String|Id|
|نام امکانات. ماکزیمم 300 کاراکتر|String|Name|
|این پارامتر دارای یکی از مقادیر "room" یا "hotel" است که مشخص کننده نوع کاربری امکانات مورد نظر است|String|Kind|

#### نمونه پاسخ برگشتی:

```javascript
{
  "api_version": "0.1.1",
  "lang": "fa_IR",
  "amenities": [
    {
      "id": "900d",
      "name": "پارکینگ",
      "kind": "hotel"
    },
    {
      "id": "b3c2",
      "name": "مینی بار",
      "kind": "room"
    }
  ]
}
```
  
  
## روش‌های پرداخت


با استفاده از این سرویس میتوانید جزییات روش­های پرداخت را دریافت کنید.

- شناسه سرویس: 51764
- پارامترهای ورودی: ندارد
- پاسخ برگشتی:json با ساختار و پارامترهای زیر:

|توضیحات|نوع|پارامتر|
|---|----|----|
|ورژن APIای که استفاده می‌شود|String|Api version|
|زبان پاسخ برگشتی|String|Lang|
|آرایه­‌ای از تمام روش‌های پرداختی که پشتیبانی می‌شود|Object[]|Payments_methods|
|شناسه منحصربفردی که برای تشخیص روش پرداخت مورد نظر استفاده میشود.این شناسه تغییرنخواهد کرد وماکزیمم 30 کاراکتر است.|String|Id|
|نام روش پرداخت. ماکزیمم 300 کاراکتر|String|Name|

#### نمونه پاسخ برگشتی:
```javascript
{
  "api_version": "0.1.1",
  "lang": "fa_IR",
  "Payments_methods": [
    {
      "id": "6571",
      "name": "credit"
    },
    {
      "id": "5d09",
      "name": "contract"
    }
  ]
}
```


## موجودی هتل


با استفاده از این سرویس میتوانید لیستی از هتل­های مد نظر کاربر را به او نشان دهید.

- شناسه سرویس: 51767
- پاسخ برگشتی:json با ساختار و پارامترهای زیر:


|توضیحات|نوع|پارامتر|
|---|----|----|
|آرایه­ای از شناسه هتل­ها برای بررسی موجودی. این شناسه­ها را میتوان از سرویس "دریافت فهرست اولیه هتل­ها" بدست آورد.|String[]|hotel_ids|
|شناسه شهر، به جای پارامتر hotel_ids میتوانید این پارامتر را ارسال کنید. این شناسه را میتوان از سرویس "دریافت اطلاعات شهرها" دریافت کرد.|String|city_id|
|تاریخ شروع (تاریخ میلادی) به صورت YYYY-MM-DD|String|start_date|
|تاریخ پایان (تاریخ میلادی) به صورت YYYY-MM-DD|String|end_date|
|با ارسال این پارامتر اطلاعات موجودی cache شده را دریافت کنید. با مقداردهی true این پارامتر پاسخ را سریعتر دریافت خواهید کرد.|Boolean|Cashe|
|این مقدار برای عیب­یابی (debugging) استفاده میشود. این مقدار log میشود.|String|query_key|
|واحد پول طبق استاندارد ISO 4217|String|currency|
|کد کشور دو حرفی طبق استاندارد ISO 3166-1 alpha-2|String|user_country|
|نوع دستگاه کاربر را مشخص میکند و میتواند مقادیر “d”, “m” یا “t” را داشته باشد که به ترتیب مربوط به DESKTOP, MOBILE و TABLET مربوط میشوند. اگر قیمت نسبت به نوع دستگاه تفاوت داشته باشد ارسال این پارامتر اجباری است.|String|device_type|


- پاسخ برگشتی: json با ساختار و پارامترهای زیر:


|توضیحات|نوع|پارامتر|
|---|----|----|
|زبان پاسخ برگشتی|String|Lang|
|آرایه‌­ای از لیست object های شامل هتل­های در دسترس. الزاما تمام هتل­های درخواست داده شده در پاسخ موجود نخواهند بود.|object[]|Hotels|
|شناسه هتل|String|Id|
||object[]|Room_types|
|شناسه نوع اتاق|String|Id|
|عنوان نوع اتاق. ماکزیمم 50 کاراکتر|String|Title|
|ماکزیمم تعداد مهمانان مجاز در اتاق|Number|Capacity|
|ماکزیمم تعداد مهمانان اضافی مجاز در اتاق|Number|extera_capacity|
|آرایه‌­ای از objectهای از نوع DatePrice. این پارامتر مشخص کننده قیمت هر روز اقامت در هتل است.|object[]|Prices|
|تاریخ این قیمت در بازه تاریخ شروع تا تاریخ پایان|String|Date|
|قیمت پایه هتل برای اتاق مورد نظر در تاریخ مشخص شده. این قیمت بدون احتساب مالیات و تخفیف است.|Number|Price|
|قیمت نهایی هتل برای تاریخ مشخص شده، این قیمت شامل مالیات، تخفیف و کارمزد است.|Number|Price_to_pay|
||Number|Price|
|قیمت کل اقامت بدون احتساب مالیات و تخفیف|Number|Price|
|مالیات کل بدون احتساب تخفیف|Number|Taxes|
|قیمت نهایی شامل قیمت کل اقامت و مالیات بدون احتساب تخفیف.توجه کنید که این مقدار قیمت نهایی زمان اقامت است که یک فرد می­بایست پرداخت کند|Number|final_price|
|قیمت نهایی که می­بایست پرداخت شود، شامل قیمت کل مدت اقامت، مالیات و تخفیف. توجه کنید این قیمتی است که شما به عنوان یک آژانس می­بایست به هتل پرداخت کنید. شما باید حاشیه سود خود را به این قیمت اضافه کنید و به مشتری نشان دهید.|Number|Price_to_Pay|
|objectهایی از اتاق­های باقی مانده. این پارامتر نشان دهنده­ی تعداد اتاق­های باقی مانده به ازای هر روز اقامت است.|object|rooms_remaining_per_day|
|تاریخ اتاق های باقی مانده در بازه تارزیخ شروع تا تاریخ پایان|Number|date|
|تعداد اتاق‌­های باقی مانده برای یک تاریخ مشخص|Number|Count|
|تعداد اتاق­های باقی مانده|String|Currency|
|واحد پول طبق استاندارد ISO 4217|object[]|Errors|
|آرایه‌ه­ای از موارد خطا|Number|Code|
|1: خطای ناشناخته...2: عدم توانایی در تفسیر درخواست...3: شناسه هتل نامعتبر...4: درخواست timeout شده...5: خطای قابل بازیابی. این خطا معادل خطای http 503 است.|Number|Code|
|توضیحات خطای رخ داده. ماکزیمم 1000 کارکتر|String[]|Message|
|در صورت دریافت error code 4 این پارامتر مقدار زمانی است (به ثانیه) که می­بایست منتظر باشید و سپس درخواست جدیدی ارسال کنید.|Number[]|Timeout|
|تعداد تخت­های از این نوع خاص در اتاق|Number|hotel_id|


#### نمونه پاسخ برگشتی

```javascript
{
  "api_version": "0.1.1",
  "lang": "fa_IR",
  "hotels": [
    {
      "id": "a3d6",
      "agency_contract": false,
      "room_types": [
        {
          "id": "d634",
          "title": "دابل دابل",
          "capacity": 2,
          "extra_capacity": 2,
          "prices": [
            {
              "date": "2017-09-20",
              "price": 3600000,
              "price_to_pay": 2912436
            }
          ],
          "price": {
            "price": 3600000,
            "taxes": 291600,
            "final_price": 3891600,
            "price_to_pay": 2912436
          },
          "rooms_remaining_per_day": [
            {
              "date": "2017-09-20",
              "count": 1
            }
          ],
          "rooms_remaining": 1
        },
        {
          "id": "d635",
          "title": "سه تخته",
          "capacity": 3,
          "extra_capacity": 0,
          "prices": [
            {
              "date": "2017-09-20",
              "price": 4950000,
              "price_to_pay": 4004599.5
            }
          ],
          "price": {
            "price": 4950000,
            "taxes": 400950,
            "final_price": 5350950,
            "price_to_pay": 4004599.5
          },
          "rooms_remaining_per_day": [
            {
              "date": "2017-09-20",
              "count": 2
            }
          ],
          "rooms_remaining": 2
        }
      ],
      "currency": "IRR"
    }
  ],
  "errors": []
}
```

## دریافت اطلاعات قیمت و موجودی هتل

زمانی که نتایج این سرویس برگردانده می­شود، این نتایج می­بایست در کنار نتایج سرویس "موجودی هتل" به مسافر نشان داده شده شود. مسافر در مرحله بعد میتواند اقدام به رزرو اتاق کند.

- شناسه سرویس: 51775
-  پارامترهای ورودی: json با پارامترهای زیر:

|توضیحات|نوع|پارامتر|
|----|----|---|
|زبان پاسخ برگشتی|String|Lang|
|شناسه هتل در لاماسو|String|Hotel_id|
|تاریخ ابتدایی (میلادی، yyyy/mm/dd)|String|Start_date|
|تاریخ پایان (میلادی، yyyy/mm/dd)|String|end_date|
|با ارسال این پارامتر میتوانید به اطلاعات cache دسترسی داشته باشید. مقدار cache را برابر true قرار دهید تا نتایج را سریعتر دریافت کنید.|Boolean|Cash|
|این پارامتر برای اشکال­زدایی (debugging) استفاده میشود. این مقدار log میشود.|String|query_key|
|واحد پول طبق استاندارد ISO 4217|String|Currency|
|کد کشور براساس استاندارد ISO 3166-1 alpha-2|String|user_country|
|نوع دستگاه کاربر را مشخص میکند و میتواند مقادیر “d”, “m” یا “t” را داشته باشد که به ترتیب مربوط به DESKTOP, MOBILE و TABLET مربوط میشوند. اگر قیمت نسبت به نوع دستگاه تفاوت داشته باشد ارسال این پارامتر اجباری است.|String|device_type|

- :پاسخ برگشتی

|توضیحات|نوع|پارامتر|
|----|----|---|
|زبان پاسخ برگشتی|String|Lang|
||Object|Hotel|
|شناسه هتل درخواستی. این شناسه همان مقدار پارامتر hotel_id است که در درخواست ارسال شده است|String|Id|
||Object|room_types|
|شناسه نوع اتاق|String|Id|
|عنوان نوع اتاق. ماکزیمم 50 کاراکتر|String|Title|
|ماکزیمم تعداد افراد مجاز در اتاق|Number|Capacity|
|ماکزیمم تعداد افراد اضافه مجاز در اتاق|Number|Extra_Capacity|
|objectهایی از اتاق­های باقی مانده. این پارامتر نشان دهنده‌­ی تعداد اتاق‌­های باقی مانده به ازای هر روز اقامت است.|String|rooms_remaininig_per_day|
|تاریخ اتاق­های باقی مانده در بازه {تاریخ ابتدایی، تاریخ پایانی}|Number|date|
|تعداد اتاق­های باقی مانده در یک تاریخ مشخص|Number|count|
|تعداد اتاق های باقی مانده|Number|rooms_remaininig|
|آرایه HotelRatePlans که برای یک هتل ثابت هستند|Object[]|rate_plans|
|شناسه Rate Plan|String|Id|
|عنوان Rate Plan. ماکزیمم 100 کاراکتر|String|Id|
|توضیحات Rate Plan. ماکزیمم 300 کاراکتر|String|Desc|
|Objectهایی از DatePrice|Number| extra_guest_cost_per_day|
|تاریخ این قیمت در بازه {تاریخ ابتدایی، تاریخ پایانی}|Number|Date|
|قیمت مازاد در این تاریخ بدون احتساب مالیات و تخفیف. این مقدار قیمت مازاد واقعی بدون تخفیف است|Number|price|
|قیمت مازاد نهایی در این تاریخ  شامل مالیات، تخفیف­ها و کارمزدها|Number|price_to_pay|
||Number|extra_guest_cost|
|قیمت کل اقامت بدون احتسلب مالیات و تخفیف­ها|Number|price|
|مالیات کل بدون احتساب تخفیف|Number|taxes|
|قیمت نهایی شامل قیمت کل اقامت و مالیات بدون احتساب تخفیف.توجه کنید که این مقدار قیمت واقعی اقامت است که یک مسافر می­بایست پرداخت کند|Number|final_price|
|قیمت نهایی که می­بایست پرداخت شود شامل هزینه اقامت، مالیات و تخفیف.توجه کنید که این مبلغی است که شما می­بایست به ما پرداخت کنید و نه مبلغ پرداختی مشتری.شما می­بایست سود خود را به این قیمت اضافه کرده و به مشتری نشان دهید|Number|price_to_pay|
|برنامه غذا|String|meal_type|
|این پارامتر مشخص میکند که این rate plan دارای انتقال هست یا خیر|String|Transfer|
|این پارامتر مشخص میکند که این rate plan که برای اضافه کردن بچه به افراد دارای نرخ نیم بها است یا خیر|String|half_extera_price|
|آرایه سیاست لغو برای این rate plan|object[]|cacellation_policies|
|بازه لغو با فرمت #h (تعداد ساعات)|String|period|
|جریمه لغو|Number|Penalty|
|نوع لغو رزرو. می­تواند به صورت درصدی یا ثابت باشد|String|Type|
|آرایه objectهای RoomRate|object[]|room_rates|
|شناسه نوع اتاق (RoomType)|String|room_type_id|
|شناسه RatePlan|String|rate_plan_id|
|آرایه objectهای DatePrice|Object[]|Price|
|تاریخ این قیمت در بازه {تاریخ ابتدایی، تاریخ پایان}|String|Date|
|قیمت اتاق در این تاریخ بدون احتساب مالیات و تخفیف. این قیمت واقعی اتاق بدون هیچگونه تخفیفی است.|Number|Amount|
|قیمت نهایی هتل در این تاریخ شامل مالیات، تخفیف و کارمزد.|Number|price_to_pay|
|آرایه objectهای RoomDiscount|Object[]|Discounts|
|متن بازاریابی برای تخفیف. مازیمم 50 کاراکتر. اختیاری.|String|marketing_text|
|این پارامتر مشخص میکند که تخفیف درصدی است یا مقدار مشخصی دارد.|boolean|is_percent|
|میزان تخفیف. اگر پارامتر is_percent برابر true باشد، آنگاه این مقدار میزان درصد است در غیر اینصورت میزان واقعی و مطلق تخفیف است.|Number|Amount|
|میزان تخفیف اعمال شده به قیمت اقامت|Number|Price|
|میزان تخفیف اعمال شده به مالیات اقامت|Number|Taxes|
|میزان تخفیف اعمال شده به قیمت نهایی اقامت|Number|final_price|
||Number|Price|
|قیمت کل اقامت بدون احتساب مالیات و تخفیف|Number|Price|
|مالیات کل بدون احتساب تخفیف|Number|Taxes|
|قیمت نهایی شامل مبلغ کل اقامت و مالیات بدون احتساب تخفیف.توجه کنید که این قیمت واقعی اقامت است که یک مسافر می­بایست برای اقامت بپردازد|Number|final_price|
|قیمت نهایی که می­بایست پرداخت شود، شامل قیمت کل مدت زمان اقامت، مالیات و تخفیف.توجه کنید این قیمتی است که شما به عنوان یک آژانس می­بایست به هتل پرداخت کنید. شما باید حاشیه سود خود را به این اضافه کنید و به مشتری نشان دهید.|Number|price_to_pay|
|واحد پول مطابق استاندارد ISO 4217|String|Currency|

#### نمونه پاسخ برگشتی:

```javascript
{
	"api_version": "0.1.1",
	"lang": "fa_IR",
	"hotel_id": "12345678",
	"room_types": [
		{
			"id": "1659",
			"title" :"اتاق یک تخته"
			"capacity": 1,
			"extra_capacity": 0,
			"rooms_remaining_per_day": [
				{
					"date": "2016-05-08",
					"count": 10
				}
			],
			"rooms_remaining": 10
		},
		{
			"id": "165b",
			"title" :"اتاق یک دو تخته",
			"capacity": 2,
			"extra_capacity": 1,
			"rooms_remaining_per_day": [
				{
					"date": "2016-05-08",
					"count": 6
				}
			],
			"rooms_remaining": 6
		}
	],
	"rate_plans": [
		{
			"id": "98c3",
			"title" :"معمولی",
			"desc" :"توضیحات",
			"extra_guest_cost_per_day": [
				{
					"date": "2016-05-08",
					"price": 2200000,
					"price_to_pay": 2200000
				}
			]
			"extra_guest_cost": {
				"price": 7000000,
				"taxes": 700000,
				"final_price": 7700000,
				"price_to_pay": 6380000
			},
			"meal_type": "BB",
			"transfer": "None",
			"half_extra_price": true,
			"cancellation_policies": [
				{
					"period": "480h",
					"penalty": "0",
					"type": "percent"
				}, 
				{
					"period": "264h",
					"penalty": "20",
					"type": "percent"
				}, 
				{
					"period": "144h",
					"penalty": "30",
					"type": "percent"
				}, 
				{
					"period": "48h",
					"penalty": "50",
					"type": "percent"
				}, 
				{
					"period": "24h",
					"penalty": "70",
					"type": "percent"
				}
			]
		}
		{
			"id": "98ff3",
			"title": "VIP",
			"desc" :"توضیحات",
			"extra_guest_cost_per_day": [
				{
				"date": "2016-05-08",
				"price": 2200000,
				"price_to_pay": 2200000
				}
			]
			"extra_guest_cost": {
				"price": 7000000,
				"taxes": 700000,
				"final_price": 7700000,
				"price_to_pay": 6380000
			},
			"meal_type": "RO",
			"transfer": "None",
			"half_extra_price": false,
			"cancellation_policies": [
				{
					"period": "480h",
					"penalty": "0",
					"type": "percent"
				}, 
				{
					"period": "264h",
					"penalty": "20",
					"type": "percent"
				}, 
				{
					"period": "144h",
					"penalty": "30",
					"type": "percent"
				}, 
				{
					"period": "48h",
					"penalty": "50",
					"type": "percent"
				}, 
				{
					"period": "24h",
					"penalty": "70",
					"type": "percent"
				}
			]
		}
	],
	"room_rates": [
		{
			"room_type_id": "1659",
			"rate_plan_id": "98c3",
			"prices": [
				{
					 "date": "2016-05-08",
					 "amount": 4000000
				},
				{
					"date": "2016-05-09",
					"amount": 3000000
				}
			],
			"discounts": [
				{
					"text_marketing" :"تخفیف ویژه آژانس",
					"is_percent": true,
					"amount": 10,
					"price": 700000,
					"taxes": 70000,
					"final_price": 770000
				},
				{
					"is_percent": false,
					"amount": 500000,
					"price": 500000,
					"taxes": 50000,
					"final_price": 550000
				}
			],
			"price": {
				"price": 7000000,
				"taxes": 700000,
				"final_price": 7700000,
				"price_to_pay": 6380000
			}
		},
		{
			"room_type_id": "165b",
			"rate_plan_id": "98c3",
			"prices": [
				{
					"date": "2016-05-08",
					"amount": 5000000
				},
				{
					"date": "2016-05-09",
					"amount": 5000000
				}
			],
			"discounts": [],
			"price": {
				"price": 10000000,
				"taxes": 1000000,
				"final_price": 11000000,
				"price_to_pay": 8880000
			}
		}
	],
	"currency": "IRR"
}
```

## موجودی هتل‌ها

با استفاده از این سرویس می‌توانید نمای کلی از هتل‌های منطبق بر سلیقه کاربر را دریافت کنید.

- شناسه سرویس: 51777
- پارامترهای ورودی:

|توضیحات|نوع|پارامتر|
|-----|-----|----|
|آرایه­‌ای از شناسه هتل­‌ها برای بررسی موجودی. این شناسه‌­ها را میتوان از سرویس "دریافت فهرست اولیه هتل­‌ها" بدست آورد.|String[]|hotel_ids|
|شناسه شهر، به جای پارامتر hotel_ids میتوانید این پارامتر را ارسال کنید. این شناسه را میتوان از سرویس "دریافت اطلاعات شهرها" دریافت کرد.|String|city_id|
|تاریخ شروع (تاریخ میلادی) به صورت YYYY-MM-DD|String|stard_date|
|تاریخ پایان (تاریخ میلادی) به صورت YYYY-MM-DD|String|end_date|
|این مقدار برای عیب‌­یابی (debugging) استفاده می‌شود. این مقدار log میشود.|String|query_key|
|واحد پول طبق استاندارد ISO 4217|String|Currency|
|کد کشور دو حرفی طبق استاندارد ISO 3166-1 alpha-2|String|user_country|
|نوع دستگاه کاربر را مشخص می‌کند و می‌تواند مقادیر “d”, “m” یا “t” را داشته باشد که به ترتیب مربوط به DESKTOP, MOBILE و TABLET مربوط می‌شوند. اگر قیمت نسبت به نوع دستگاه تفاوت داشته باشد ارسال این پارامتر اجباری است.|String|device_type|


- پاسخ برگشتی:

|توضیحات|نوع|پارامتر|
|-----|-----|-----|
|زبان پاسخ برگشتی|String|Lang|
|آرایه­‌ای از object های موجودی هتل. الزاما تمام هتل­‌های درخواستی در پاسخ این سرویس موجود نیستند.|Object[]|Hotels|
|شناسه هتل|String|Id||
||Object[]|room_types|
|شناسه نوع اتاق|String|Id|
|عنوان نوع اتاق. ماکزیمم 50 کاراکتر|Sting|title|
|ماکزیمم نفرات مجاز در اتاق|Number|capacity|
|ماکزیمم نفرات اضافه در اتاق|Number|extra_capacity|
|آرایه­‌ای از object های ا‌‌‌تا‌ق­های باقیمانده. این پارامتر تعداد ا‌‌تاق­های باقیمانده برای هر روز از اقامت را نشان می­دهد.|Object|rooms_remaining_per_day|
|تاریخ اتاق­های باقیمانده در بازه {تاریخ شروع، تاریخ پایان}|Number|date|
|تعداد اتاق­های باقیمانده در یک تاریخ مشخص|Number|count|
|تعداد اتاق­‌های باقیمانده|Number|rooms_remaining|
|آرایه‌­ای از object های تاریخ-قیمت. این پارامتر قیمت هر روز اقامت را مشخص می­‌کند|Object[]|prices|
|تاریخ قیمت ارائه شده در بازه {تاریخ شروع، تاریخ پایان}|String|date|
|قیمت پایه هتل برای این نوع اتاق در تاریخ مشخص شده. قیمت پایه اتاق در این تاریخ بدون احتساب مالیات و تخفیف.|Number|price|
|قیمت نهایی هتل در این تاریخ شامل مالیات، تخفیف و کارمزد|Number|price_to_pay|
||Object[]|price|
|قیمت کل زمان اقامت بدون احتساب مالیات و تخفیف.|Number|price|
|مالیات کل بدون احتساب تخفیف|Number|taxes|
|قیمت نهایی شامل قیمت کل مدت زمان اقامت به اضافه مالیات بدون احتساب تخفیف.توجه داشته باشید که این مقدار قیمت واقعی مدت زمان اقامت است که یک مشتری می­بایست بپردازد.|Number|final_price|
|قیمت نهایی که می­بایست پرداخت شود، شامل قیمت کل مدت زمان اقامت، مالیات و تخفیف.توجه کنید این قیمتی است که شما به عنوان یک آژانس می­بایست به هتل پرداخت کنید. شما باید حاشیه سود خود را به این قیمت اضافه کنید و به مشتری نشان دهید.|Number|price_to_pay|
|HotelRatePlan پیشفرض این مقدار برای یک هتل ثابت است.|Object[]|rate_plan|
|شناسه Rate Plan|String|Id|
|عنوان Rate Plan. ماکزیمم 100 کاراکتر|String|Title|
|توضیحات Rate Plan. ماکزیمم 300 کاراکتر|String|Desc|
|آرایه‌­ای از object های تاریخ-قیمت|Number|extra_guest_cost_per_day|
|تاریخ قیمت ارائه شده در بازه {تاریخ شروع، تاریخ پایان}|Number|Date|
|قیمت مازاد در این تاریخ بدون احتساب مالیات و تخفیف. این مقدار، قیمت مازاد واقعی بدون تخفیف است.|Number|Price|
|قیمت مازاد نهایی هتل در این تاریخ شامل مالیت، تخفیف و کارمزد.|Number|price_to_pay|
||Number|extra_guest_cost|
|قیمت کل مدت زمان اقامت بدون احتساب مالیات و تخفیف|Number|Price|
|مالیات کل بدون احتساب تخفیف|Number|Taxes|
|قیمت نهایی شامل قیمت کل مدت زمان اقامت به اضافه مالیات بدون احتساب تخفیف.توجه داشته باشید که این مقدار قیمت واقعی مدت زمان اقامت است که یک مشتری می­بایست بپردازد.|Number|final_price|
|قیمت نهایی که می­بایست پرداخت شود، شامل قیمت کل مدت اقامت، مالیات و تخفیف.  توجه کنید این قیمتی است که شما می­بایست به ما پرداخت کنید و نه قیمت پرداختی مشتری. شما باید حاشیه سود خود را به این قیمت اضافه کنید و به مشتری نشان دهید.||price_to_pay|
|برنامه غذایی|String|meal_type|
|این پارامتر مشخص می­کند که آیا این rate plan قابل انتقال است یا نه|String|transfer|
|این پارامتر مشخص می­کند که این rate plan دارای قیمت نیم بها برای کودکان هست یا نه|String|half_extra_price|
|آرایه­ سیاست­های لغو برای این rate plan|Object[]|cancellation_policies|
|بازه لغو در فرمت #h|String|period|
|جریمه لغو|String|penalty|
|نوع لغو، می­تواند به صورت درصدی یا ثابت است.|String|Type|
|نوع ارز طبق استاندارد ISO 4217|String|currency|
|آرایه object های خطا|Object[]|errors|
|1: Unknown Error.2: Cannot Parse Request.3: Invalid Hotel ID.4: Timeout requested.Ask to requests for thespecified time.5: Recoverable Error. Equivalent to http 503.|Number|Code|
|رشته توصیف کننده خطا. می­توان برای عیب‌­یابی از این پیام استفاده کرد. ماکزیمم 1000 کاراکتر|String[]|message|
|تعداد ثانیه‌­های انتظار برای ارسال درخواست جدید. مرتبط با error code 4|Number[]|Timeout|
|شناسه هتلی که این خطا مربوط به آن است.|String[]|hotel_id|



#### نمونه پاسخ برگشتی:

```javascript
{
  "lang": "fa_IR",
  "currency": "IRR",
  "hotels": [
    {
      "id": "a3d6",
      "agency_contract": false,
      "room_types": [
        {
          "id": "d634",
          "title": "دابل دابل",
          "capacity": 2,
          "extra_capacity": 2,
          "rooms_remaining_per_day": [
            {
              "date": "2020-09-20",
              "count": 1
            }
          ],
          "rooms_remaining": 1,
          "prices": [
            {
              "date": "2020-09-20",
              "price": 3600000,
              "price_to_pay": 2912436
            }
          ],
          "price": {
            "price": 3600000,
            "taxes": 291600,
            "final_price": 3891600,
            "price_to_pay": 2912436
          }
        },
        {
          "id": "d635",
          "title": "سه تخته کلاسیک",
          "capacity": 3,
          "extra_capacity": 0,
          "prices": [
            {
              "date": "2020-09-20",
              "price": 4950000,
              "price_to_pay": 4004599.5
            }
          ],
          "price": {
            "price": 4950000,
            "taxes": 400950,
            "final_price": 5350950,
            "price_to_pay": 4004599.5
          },
          "rooms_remaining_per_day": [
            {
              "date": "2020-09-20",
              "count": 2
            }
          ],
          "rooms_remaining": 2
        }
      ],
      "currency": "IRR"
    }
  ],
  "errors": []
}

```

## ثبت اولیه رزرو همگام


این سرویس اتاق­های درخواست داده شده در هتل را در صورت امکان به صورت موقت رزرو می­کند و می­بایست توسط مشتری نگهداری شود. توجه کنید که این سرویس در صورت موفقیت­آمیز بودن، مبلغ را از اعتبار شما کسر خواهد کرد.

* شناسه سرویس: 51789
* پارامترهای ورودی:

|توضیحات|اختیاری|نوع|پارامتر|
|----|---|----|----|
|تاریخ ورود به هتل (YYYY-MM-DD)||String|chekin_date|
|تاریخ خروج (YYYY-MM-DD)||String|chekout_date|
|ساعت ورود (HH:MM)|بله|String|entrance_time|
|شناسه هتل||String|hotel_id|
|شناسه یکتا که توسط اپلیکیشن شما تولید می­شود||String|refrence_id|
|شناسه روش پرداخت مورد نظر. اگر این پارامتر ارسال نشود، روش پرداخت پیشفرض سیستم بر اساس قرارداد شما با هتل اعمال خواهد شد، روش بر پایه اعتبار یا قرارداد.|بله|String|payment_method|
|اطلاعات مشتری||Object|Customer|
|نام مشتری||String|first_name|
|نام خانوادگی مشتری||String|last_name|
|کد ملی مشتری||String|national_code|
|شماره پاسپورت مشتری، توجه کنید که یکی از مقادیر کد ملی یا شماره پاسپورت الزامی است.|بله|String|passport_num|
|شماره تلفن مشتری||String|phone_number|
|آدرس ایمیل مشتری|بله|String|Email|
|کد کشور مبدا مشتری مطابق با استاندارد ISO 3166-1 alpha-2||String|Country|
|آدرس مشتری|بله|String|Address|
|میتواند یکی از این مقادیر باشد: Car, Train, Bus, Airplane, Other.این پارامتر برای سرویس حمل و نقل هتل اجباری است.|بله|String|vehicle|
|اگر وسیله نقلیه یکی از موارد قطار، هواپیما یا اتوبوس باشد این مقدار اجباری است.|بله|String|vehicle_code|
|آرایه اتاق­‌هایی که می­بایست رزرو شوند.||Object[]|Rooms|
|||Number|Type_id|
|تعداد مهمانان||Object|Party|
|تعداد بزرگسالان||Number|Adults|
|تعداد کودکان به همراه سن آنها||Object[]|Children|
|مشخصات مهمانان برای نوع اتاق کنونی|بله|Object[]|Guests|
|نام مهمان||String|first_name|
|نام­ خانوادگی مهمان||String|last_name|
|کد ملی مهمان||String|national_code|
|شماره پاسپورت مهمان. توجه کنید که یکی از مقادیر کد ملی یا شماره پاسپورت الزامی است|بله|String|شماره پاسپورت|
|شماره تلفن مهمان||String|phone_number|
|آدرس ایمیل مهمان|بله|String|Email|
|کد کشور مبدا مشتری مهمان مطابق با استاندارد ISO 3166-1 alpha-2||String|country|
|آدرس مهمان|بله|String|Address|
|میتواند یکی از این مقادیر باشد: Car, Train, Bus, Airplane, Other.این پارامتر برای سرویس حمل و نقل هتل اجباری است.|بله|String|Vehicle|
|اگر وسیله نقلیه یکی از موارد قطار، هواپیما یا اتوبوس باشد این مقدار اجباری است.|بله|String|Vehicle_code|
|||Number|rate_plan_id|
|درخواست­ها یا نظرات خاص مسافر برای هتل|بله|String|special_requests|


* پاسخ برگشتی:

|توضیحات|نوع|پارامتر|
|----|----|----|
|Success/Failure|String|Status|
|شماره پیگیری آژانس|String|reference_id|
|جزییات درگاه پشتیبان پرداخت|Object|payment_details|
|مبلغ قابل پرداخت رزرو. این مقدار برابر است با جمع سهم هتل و سهم لاماسو|Number|price_to_pay|
|قیمت کل رزرو در هتل|Number|hotel_share|
|میزان کارمزدی که لاماسو از رزرواسیون برمی­دارد.|Number|lamasoo_share|
|شناسه فاکتور رزرو|Number|invoice|
|URL درگاه بانکی فاکتور. این پارامتر اختیاری است||URL|
||Object|customer_support|
||String|phone_number|
||String|Email|


#### نمونه پاسخ برگشتی:

```javascript

HTTP/1.1 200 OK
{
	"problems": [],
	"status": "Success",
	"reference_id": "ref-3129304",
	"payment_detail": {
		"price_to_pay": 27802521,
		"hotel_share": 27664200,
		"lamasoo_share": 138321,
		"invoice": 9526608,
		"URL": "https://payment-gateway.com/?invoiceId=835&redirectUri=http://lamasoo.com"
	}
	"customer_support": {
		"phone_number": "02112345678",
		"email": "hotel@example.com"
	}
}

```

#### خطاهای این سرویس:

|توضیحات|نوع|پارامتر|
|----|----|-----|
|1: Unknown Error.2: Cannot Parse Request.3: Invalid Hotel ID.4: Timeout requested. Ask to requests for the specified time.5: Recoverable Error. Equivalent to http 503.6: You haven't defined any contracts with the given hotel.7: Unable to retrieve hotel's data.8: Invalid RoomType ID.9: Over capacity.10: Duplicate reference ID.11: No available room is remaining.12: No reservation found.13: Credit is not enough for reservation|Number|code|
|توضیحات خطای رخ داده. این پارامتر برای عیب‌­یابی استفاده می­شود. ماکزیمم 1000 کاراکتر|String|message|
|تعداد ثانیه‌­های انتظار برای ارسال درخواست جدید. مرتبط با error code 4|Nember|Timeout|


## ثبت رزرو ناهمگام



این سرویس اتاق­های درخواست داده شده در هتل را در صورت امکان به صورت موقت رزرو می­کند و می­بایست توسط مشتری نگهداری شود. توجه کنید که این سرویس در صورت موفقیت­آمیز بودن، مبلغ را از اعتبار شما کسر خواهد کرد.

* شناسه سرویس: 51792
* پارامترهای ورودی: 

|توضیحات|اختیاری|نوع|پارامتر|
|----|---|----|----|
|تاریخ ورود به هتل (YYYY-MM-DD)||String|chekin_date|
|تاریخ خروج (YYYY-MM-DD)||String|chekout_date|
|ساعت ورود (HH:MM)|بله|String|entrance_time|
|شناسه هتل||String|hotel_id|
|شناسه یکتا که توسط اپلیکیشن شما تولید می­شود||String|refrence_id|
|شناسه روش پرداخت مورد نظر. اگر این پارامتر ارسال نشود، روش پرداخت پیشفرض سیستم بر اساس قرارداد شما با هتل اعمال خواهد شد، روش بر پایه اعتبار یا قرارداد.|بله|String|payment_method|
|اطلاعات مشتری||Object|Customer|
|نام مشتری||String|first_name|
|نام خانوادگی مشتری||String|last_name|
|کد ملی مشتری||String|national_code|
|شماره پاسپورت مشتری، توجه کنید که یکی از مقادیر کد ملی یا شماره پاسپورت الزامی است.|بله|String|passport_num|
|شماره تلفن مشتری||String|phone_number|
|آدرس ایمیل مشتری|بله|String|Email|
|کد کشور مبدا مشتری مطابق با استاندارد ISO 3166-1 alpha-2||String|Country|
|آدرس مشتری|بله|String|Address|
|میتواند یکی از این مقادیر باشد: Car, Train, Bus, Airplane, Other.این پارامتر برای سرویس حمل و نقل هتل اجباری است.|بله|String|vehicle|
|اگر وسیله نقلیه یکی از موارد قطار، هواپیما یا اتوبوس باشد این مقدار اجباری است.|بله|String|vehicle_code|
|آرایه اتاق­‌هایی که می­بایست رزرو شوند.||Object[]|Rooms|
|||Number|type_id|
|تعداد مهمانان||Object|Party|
|تعداد بزرگسالان||Number|Adults|
|تعداد کودکان به همراه سن آنها||Object[]|Children|
|مشخصات مهمانان برای نوع اتاق کنونی|بله|Object[]|Guests|
|نام مهمان||String|first_name|
|نام­ خانوادگی مهمان||String|last_name|
|کد ملی مهمان||String|national_code|
|شماره پاسپورت مهمان. توجه کنید که یکی از مقادیر کد ملی یا شماره پاسپورت الزامی است|بله|String|شماره پاسپورت|
|شماره تلفن مهمان||String|phone_number|
|آدرس ایمیل مهمان|بله|String|Email|
|کد کشور مبدا مشتری مهمان مطابق با استاندارد ISO 3166-1 alpha-2||String|country|
|آدرس مهمان|بله|String|Address|
|میتواند یکی از این مقادیر باشد: Car, Train, Bus, Airplane, Other.این پارامتر برای سرویس حمل و نقل هتل اجباری است.|بله|String|Vehicle|
|اگر وسیله نقلیه یکی از موارد قطار، هواپیما یا اتوبوس باشد این مقدار اجباری است.|بله|String|Vehicle_code|
|||Number|rate_plan_id|
|درخواست­ها یا نظرات خاص مسافر برای هتل|بله|String|special_requests|


* پاسخ برگشتی:

|توضیحات|نوع|پارامتر|
|----|----|----|
|Success/Failure|String|Status|
|شماره پیگیری آژانس|String|reference_id|
|جزییات درگاه پشتیبان پرداخت|Object|payment_details|
|مبلغ قابل پرداخت رزرو. این مقدار برابر است با جمع سهم هتل و سهم لاماسو|Number|price_to_pay|
|قیمت کل رزرو در هتل|Number|hotel_share|
|میزان کارمزدی که لاماسو از رزرواسیون برمی­دارد.|Number|lamasoo_share|
|شناسه فاکتور رزرو|Number|invoice|
|URL درگاه بانکی فاکتور. این پارامتر اختیاری است||URL|
|جزییات قیمت اتاق‌های رزرو شده|Object|price_details|
|قیمت اتاق‌های رزرو شده|Object[]|Rooms|
|شناسه اتاق|String|Id|
|قیمت کل اتاق|String|Price|
|قیمت اتاق به ازای هر روز اقامت|Object[]|Prices|
| تاریخ (YYYY-MM-DD)|String|Date|
|قیمت در تاریخ مورد نظر|Number|Price|
|قیمت مازاد کل مربوط به اتاق|Number|extra_price|
|کارمزد سرویس رزرو کل|Object[]|Wage|
||Object|customer_support|
||String|phone_number|
||String|Email|


#### نمونه پاسخ برگشتی:

```javascript

HTTP/1.1 200 OK
{
  "problems": [],
  "status": "Success",
  "reference_id": "refId-81",
  "payment_details": {
    "price_to_pay": 27802521,
    "hotel_share": 27664200,
    "lamasoo_share": 138321,
    "invoice": 9526608,
    "URL": ""
  },
  "price_details": {
    "rooms": [
      {
        "id": "58a9b898dd068f2c5dcaf906",
        "price": 10006200,
        "prices": [
          {
            "date": "2020-04-20",
            "price": 3335400
          },
          {
            "date": "2020-04-21",
            "price": 3335400
          },
          {
            "date": "2020-04-22",
            "price": 3335400
          }
        ],
        "extra_price": 0
      },
      {
        "id": "58a9b898dd068f2c5dcaf906",
        "price": 10006200,
        "prices": [
          {
            "date": "2020-04-20",
            "price": 3335400
          },
          {
            "date": "2020-04-21",
            "price": 3335400
          },
          {
            "date": "2020-04-22",
            "price": 3335400
          }
        ],
        "extra_price": 0
      },
      {
        "id": "58a9b898dd068f2c5dcaf905",
        "price": 7651800,
        "prices": [
          {
            "date": "2020-04-20",
            "price": 2550600
          },
          {
            "date": "2020-04-21",
            "price": 2550600
          },
          {
            "date": "2020-04-22",
            "price": 2550600
          }
        ],
        "extra_price": 0
      }
    ],
    "wage": 138321
  },
  "customer_support": {
    "phone_number": "05132220320",
    "email": "info@hotelreza.ir"
  }
}

```

#### خطاهای این سرویس:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|1: Unknown Error.2: Cannot Parse Request.3: Invalid Hotel ID.4: Timeout requested. Ask to requests for the specified time.5: Recoverable Error. Equivalent to http 503.6: You haven't defined any contracts with the given hotel.7: Unable to retrieve hotel's data.8: Invalid RoomType ID.9: Over capacity.10: Duplicate reference ID.11: No available room is remaining.12: No reservation found.13: Credit is not enough for reservation|Number|Code|
|توضیحات خطای رخ داده. این پارامتر برای عیب‌­یابی استفاده می­شود. ماکزیمم 1000 کاراکتر|String|message|
|تعداد ثانیه­های انتظار برای ارسال درخواست جدید. مرتبط با error code 4|Number|Timeout|


## تایید رزرو همگام

 این سرویس، درخواست رزرو ثبت شده توسط سرویس "ثبت رزرو همگام" را تایید و یک شماره رزرو که توسط هتل صادر شده است برمی­گرداند و می­بایست توسط مشتری نگهداری شود. توجه کنید که این سرویس در صورت موفقیت­آمیز بودن از موجودی حساب شما کسر می­کند.

* شناسه سرویس: 51795
* پارامترهای ورودی:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|شناسه هتل درخواستی|String|hotel-id|
|شناسه‌­ای که در سرویس ثبت رزرو ارسال کردید.|String|refernce_id|


* پاسخ برگشتی:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|وضعیت کلی درخواست تایید رزرو. شامل یکی از موارد زیر:Success, Failure, UnknownReference|String|status|
|شناسه‌­ای که توسط هتل صادر شده و به عنوان معرف این رزرو شناخته میشود.این پارامتر تنها در صورتی که رزرو به صورت موفقیت‌­آمیز تایید شود در پاسخ وجود خواهد داشت.|String|reservation_id|

#### نمونه پاسخ برگشتی:

```javascipt
HTTP/1.1 200 OK
{
	"api_version": "0.1.1",
	"status": "success",
	"reservation_id": 250
}

```

#### خطاهای این سرویس:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|1: Unknown Error.2: Cannot Parse Request.3: Invalid Hotel ID.4: Timeout requested. Ask to requests for the specified time.5: Recoverable Error. Equivalent to http 503.6: You haven't defined any contracts with the given hotel.7: Unable to retrieve hotel's data.8: Invalid RoomType ID.9: Over capacity.10: Duplicate reference ID.11: No available room is remaining.12: No reservation found.13: Credit is not enough for reservation.14: No response from hotel.15: The invoice is not paid.|Number|Code|
|توضیحات خطای رخ داده. این پارامتر برای عیب‌­یابی استفاده می­شود. ماکزیمم 1000 کاراکتر|String|Message|
|تعداد ثانیه‌­های انتظار برای ارسال درخواست جدید. مرتبط با error code 4|Number|Timeout|



## تایید رزرو ناهمگام

این سرویس، درخواست رزرو ثبت شده توسط سرویس "ثبت رزرو ناهمگام" را تایید و یک شماره رزرو که توسط هتل صادر شده است برمی­گرداند و می­بایست توسط مشتری نگهداری شود. توجه کنید که این سرویس در صورت موفقیت­آمیز بودن از موجودی حساب شما کسر می­کند.

* شناسه سرویس: 51797
* پارامترهای ورودی:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|شناسه هتل درخواستی|String|hotel_id|
|شناسه­‌ای که در سرویس ثبت رزرو ارسال کردید.|String|reference_id|

* پاسخ برگشتی:


|توضیحات|نوع|پارامتر|
|-----|----|----|
|وضعیت کلی درخواست تایید رزرو. شامل یکی از موارد زیر:hotel-confirmed, lamasoo-confirmed|String|
status|
|شناسه‌­ای که توسط هتل صادر شده و به عنوان معرف این رزرو شناخته میشود.این پارامتر تنها در صورتی که رزرو به صورت موفقیت­‌آمیز تایید شود در پاسخ وجود خواهد داشت.|String|reservation_id|

#### نمونه پاسخ برگشتی:

```javascript
HTTP/1.1 200 OK
{
	"api_version": "0.1.1",
	"status": "hotel-confirmed",
	"reservation_id": 250
}
```

#### خطاهای این سرویس:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|1: Unknown Error.2: Cannot Parse Request.3: Invalid Hotel ID.4: Timeout requested. Ask to requests for the specified time.5: Recoverable Error. Equivalent to http 503.6: You haven't defined any contracts with the given hotel.7: Unable to retrieve hotel's data.8: Invalid RoomType ID.9: Over capacity.10: Duplicate reference ID.11: No available room is remaining.12: No reservation found.13: Credit is not enough for reservation.14: No response from hotel.15: The invoice is not paid.|Number|Code|
|توضیحات خطای رخ داده. این پارامتر برای عیب‌یابی استفاده می­شود. ماکزیمم 1000 کاراکتر|String|Message|
|تعداد ثانیه‌­های انتظار برای ارسال درخواست جدید. مرتبط با error code 4|Number|timeout|


## بررسی رزرو


این سرویس برای پیگیری‌های آتی قابل استفاده است. برای استفاده از این متد باید کد رفرنسی که پیش از این در سرویس­های ثبت رزرو و تایید در فیلد refrence_id تبادل شده است و hotel_id ارسال شود.

* شناسه سرویس: 51799
* پارامترهای ورودی:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|شناسه هتل درخواستی|String|Status|
|شناسه­‌ای که در سرویس ثبت رزرو ارسال کردید.|String|reference_id|

* پاسخ برگشتی:

|توضیحات|نوع|پارامتر|
|-----|----|----|
|وضعیت کلی درخواست تایید رزرو. شامل یکی از موارد زیر:Success, Failure, UnknownReference|String|Status|
|Object شامل جزییات رزرو (رسید، تاریخ اقامت، مهمانان و...). این پارامتر در صورتی که رزرو به صورت موفقیت‌­آمیز انجام شده باشد در پاسخ وجود خواهد داشت.|Object|Reservation|
|Object شامل‌ اطلاعات تماس پشتیبانی مشتری هتل برای مهمانان. این پارامتر در صورت موفق یا ناموفق بودن رزرو در پاسخ وجود خواهد داشت.|Object|Customer_support|


#### نمونه پاسخ برگشتی:
```javascript
HTTP/1.1 200 OK
{
  "problems": [],
  "status": 200,
  "reservation": {
    "agency": "TestAgency",
    "hotel": "",
    "reference_id": "134718",
    "checkin_date": "2017-08-30",
    "checkout_date": "2017-08-31",
    "entrance_time": "10:10",
    "customer": {
      "firstName": "Test",
      "lastName": "Test",
      "nationalCode": "001233456",
      "passportNum": "12345678",
      "phoneNumber": "09191234567",
      "country": "IR",
      "address": ""
    },
    "rooms": [
      {
        "roomType": "698e",
        "count": 1,
        "party": {
          "adults": 1,
          "children": []
        }
      }
    ],
    "party": {
      "adults": 1,
      "children": 0
    },
    "rate_plan_id": "1721",
    "price": 6411480,
    "confirmed": true
  },
  "customer_support": {
    "phone_number": "02112345678",
    "email": "hotel@example.com"
  }
}

```


#### خطاهای این سرویس

|توضیحات|نوع|پارامتر|
|-----|----|----|
|1: Unknown Error.
2: Cannot Parse Request.
3: Invalid Hotel ID.4: Timeout requested. Ask to requests for the specified time.5: Recoverable Error. Equivalent to http 503.6: You haven't defined any contracts with the given hotel.7: Unable to retrieve hotel's data.|Number|Code|
|توضیحات خطای رخ داده. این پارامتر برای عیب‌یابی استفاده می­شود. ماکزیمم 1000 کاراکتر|String|Message|
|تعداد ثانیه‌­های انتظار برای ارسال درخواست جدید. مرتبط با error code 4|Number|Timeout|



## لغو رزرو

این سرویس درخواست رزروی را که توسط سرویس "تایید رزرو" تایید شده است را لغو می­کند و در پاسخ سیاست­های لغو و میزان جریمه لغو را برمی­گرداند.

* شناسه سرویس: 51800

* پارامترهای ورودی:

|توضیحات|نوع|پارامتر|
|----|----|---|
|شناسه هتل درخواستی|string|hotel_id|
|شناسه‌­ای که در سرویس ثبت رزرو ارسال کردید.|string|reference_id|
|جریمه محاسبه شده آژانس- این پارامتر اختیاری است|string|Penalty|


* پاسخ برگشتی:

|توضیحات|نوع|پارامتر|
|----|----|---|
|وضعیت کلی درخواست تایید رزرو. شامل یکی از موارد زیر:Success, Failure|String|Status|
|مبلغ کل جریمه که آژانس می­بایست پرداخت کند.|Number|Penalty|


#### نمونه پاسخ برگشتی:

```javascript
HTTP/1.1 200 OK
{
	"status": "success",
	"penalty": 638522
}
```

