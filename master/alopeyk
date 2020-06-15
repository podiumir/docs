- [مقدمه](#menu)
- [پیش از شروع](#menu)
- [سرویس دریافت آدرس](#menu)
- [سرویس پیشنهادات مکان](#menu)
- [سرویس های استعلام قیمت](#menu)
- [سرویس قیمت دسته ای](#menu)
- [سفارشات](#menu)
- [سرویس ایجاد سفارش](#menu)
- [سرویس دریافت جزئیات سفارش](#menu)
- [سرویس لغو سفارش](#menu)
- [مقادیر وضعیت سفارش](#menu)
- [سرویس ویرایش سفارش](#menu)
- [خطا ها](#menu)

## مقدمه

با استفاده از api الوپیک، کسب و کار ها می توانند به راحتی خدمات تحویل بر اساس تقاضای ما را در پلتفرم خود ادغام کنند چه یک پلتفرم تجارت الکترونیک مانند Magento, Prestashop, OpenCart, WooCommerce یا ... داشته باشند چه خود توسعه دهنده برنامه خود باشند.

این api به این منظور طراحی شده که به توسعه دهندگان اجازه بررسی قیمت گذاری ما، ایجاد سفارش و رهگیری به روز رسانی های مربوط به آن سفارش را تا زمان اتمام بدهد.

<div class="box-end">
</div>

## پیش از شروع
* URL فراخوانی سرویس ها: https://api.pod.ir/srv/sc/nzh/doServiceCall
* تمامی درخواست ها با متد POST ارسال می­شوند.
* Header درخواست:
پارامترهای زیر در Header تمام درخواست ها ثابت است:

|           پارامتر    |    توضیحات                                 |
|----------------------|---------------------------------------------|
|    \_token\_    |    API token دریافتی از پنل کسب و کاری    |
|    \_token_issuer\_    |    این پارامتر دارای مقدار ثابت "1" است.    |
|    Content-Type    |    application/x-www-form-urlencoded    |


* بدنه درخواست:
پارامترهای زیر در بدنه تمام درخواست ها ثابت است:

|    پارامتر    |    توضیحات    |
|-------------------|----------------------------------------------------------------|
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

## سرویس دریافت آدرس
این سرویس اطلاعات مکانی را با طول و عرض جغرافیایی بازیابی می کند.
* شناسه سرویس: 43049
* پارامترهای ورودی:
	* lat: طول جغرافیایی
	* lng: عرض جغرافیایی
* نمونه پاسخ برگشتی یک json به شکل زیر خواهد بود:

```javascript
{
"status": "success",
"message": "findPlace",
"object": {
"address": [
"بیستم",
"گاندی جنوبی",
"ایران"
],
"region": "ونک",
"district": "",
"city": "tehran",
"traffic_zone": {
"congestion": false,
"odd_even": false
},
"city_fa": "تهران",
"province": "تهران"
}
}
```

<div class="box-end">
</div>

## سرویس پیشنهادات مکان

این سرویس آدرس ها و مکان های پیشنهادی را طبق مکان ورودی بازیابی می کند. پاسخ این سرویس مجموعه ای از مکان های پیشنهادی خواهد بود. که هر یک منطقه، نام مکان بازیابی شده و مختصات مربوط به آن را ارائه میدهد.
* شناسه سرویس: 43052
* پارامترهای ورودی:
	* region: نام منطقه مورد نظر.
* نمونه پاسخ برگشتی برای ورودی "میرداماد" به شکل زیر است:

```javascript
{
"status": "success",
"message": "autoComplete",
"object": [
{
"title": "میرداماد",
"region": "شیوا",
"lat": "35.680097111817098",
"lng": "51.466359241720198",
"district": "منطقه ۱۴",
"city": "tehran",
"city_fa": "تهران"
},
{
"title": "میرداماد",
"region": "مینایی",
"lat": "35.654716852415099",
"lng": "51.4560997326357",
"district": "منطقه ۱۵",
"city": "tehran",
"city_fa": "تهران"
},
{
"title": "میرداماد",
"region": "داودیه",
"lat": "35.760104930870803",
"lng": "51.432777284209102",
"district": false,
"city": "tehran",
"city_fa": "تهران"
},
{
"title": "میرداماد",
"region": "tehran",
"lat": "35.5386945664753",
"lng": "51.2160959801693",
"district": false,
"city": "tehran",
"city_fa": "تهران"
},
{
"title": "بلوار میرداماد",
"region": "داودیه",
"lat": "35.7600557285908",
"lng": "51.431922949816098",
"district": false,
"city": "tehran",
"city_fa": "تهران"
}
]
}
```

<div class="box-end">
</div>

## سرویس های استعلام قیمت
### سرویس قیمت عادی

این سرویس اطلاعات محاسبه قیمت برای یک جفت (طول و عرض جغرافیایی) را بازیابی می کند.
* شناسه سرویس: 43074
* پارامترهای ورودی:
	* body: یک json با ساختار و پارامترهای زیر:

|     پارامتر               	|     پیش فرض    	|     ضروری    	|     توضیحات                                                                                                                                                                                                                           	|
|---------------------------	|----------------	|--------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|     transport_type        	|     NULL       	|     TRUE     	|     نوع حمل و نقل سفارش. در حال حاضر مقادیر معتبر برای این ویژگی   عبارتند از: motorbike برای تحویل بسته های ساده ، motor_taxi برای   حمل و نقل مسافر ، cargo برای محموله ، cargo_s برای محموله های کوچک ، و ماشین برای حمل و نقل.    	|
|     addresses[0][type]    	|     NULL       	|     true     	|     باید از نوع origin باشد                                                                                                                                                                                                           	|
|     addresses[0][lat]     	|     NULL       	|     true     	|     عرض از origin آدرس                                                                                                                                                                                                                	|
|     addresses[0][lng]     	|     NULL       	|     true     	|     طول از origin آدرس                                                                                                                                                                                                                	|
|     addresses[1][type]    	|     NULL       	|     true     	|     باید از نوع destination باشد                                                                                                                                                                                                      	|
|     addresses[1][lat]     	|     NULL       	|     true     	|     عرض جغرافیایی آدرس destination اول.                                                                                                                                                                                               	|
|     addresses[1][lng]     	|     NULL       	|     true     	|     طول جغرافیایی آدرس destination اول.                                                                                                                                                                                               	|
|     addresses[2][type]    	|     NULL       	|     false    	|     باید از نوع destination باشد.                                                                                                                                                                                                     	|
|     addresses[2][lat]     	|     NULL       	|     false    	|     عرض جغرافیایی آدرس های destination اضافی                                                                                                                                                                                          	|
|     addresses[2][lng]     	|     NULL       	|     false    	|     طول جغرافیایی آدرس های destination اضافی                                                                                                                                                                                          	|
|     has_return            	|     false      	|     false    	|     اگر تمایل به محاسبهحاسبه سفارشی دارید که گزینه return دارد این مقدار را true تنظیم کنید                                                                                                                                           	|
|     cashed                	|     false      	|     false    	|     اگر تمایل دارید نوع پرداخت ضرورتا نقدی باشد این مقدار را true تنظیم کنید.                                                                                                                                                         	|
|     optimize              	|     false      	|     false    	|     یک مسیر بهینه را تخمین بزنید و. این مقدار را true تنظیم کنید تا در محاسبات قیمت   استفاده شود.                                                                                                                                    	|

*  نمونه json ارسالی:

```javascript
{
"transport_type": "motor_taxi",
"addresses": [
{
"type": "origin",
"lat": "35.755460",
"lng": "51.416874"
},
{
"type": "destination",
"lat": "35.758495",
"lng": "51.442550"
},
{
"type": "destination",
"lat": "35.895452",
"lng": "51.589632"
}
],
"has_return": false,
"cashed": false
}
```
* پاسخ برگشتی: یک json با ساختار و پارامترهای زیر:
*
|     پارامتر              	|     توضیحات                                                                                                                                                                                                                           	|
|--------------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|     status               	|     نشان می دهد که پیشرفت محاسبه موفقیت آمیز بوده یا خیر.                                                                                                                                                                             	|
|     price                	|     قیمت محاسبه شده کل.                                                                                                                                                                                                               	|
|     credit               	|     نوع پرداخت سفارش را نشان می دهد (پرداخت با اعتبار یا پول نقد).   فقط درصورتی که اعتبار کافی در حساب خود برای آن سفارش داشته باشید صادق خواهد   بود. در صورت کمبود اعتبار یا اینکه cashed=true باشد این ویژگی false   خواهد بود    	|
|     distance             	|     تخمین فاصله بین منبع و مقصد                                                                                                                                                                                                       	|
|     duration             	|     مدت زمان تخمینی از مسیر بین مبدا و مقصد                                                                                                                                                                                           	|
|     user_credit          	|     اعتبار فعلی شما (به تومان).                                                                                                                                                                                                       	|
|     price_with_return    	|     قیمت محاسبه شده برای سفارش ، در صورتیکه has_return   = true   باشد                                                                                                                                                                	|

نمونه پاسخ برگشتی:
```javascript
{
"status": "success",
"message": null,
"object": {
"addresses": [
{
"type": "origin",
"lat": 35.75678,
"lng": 51.411255,
"address": "تهران، منطقه ۳، کاووسیه، خ گاندی، خ بیستم",
"city": "tehran",
"city_fa": "تهران",
"priority": 0
},
{
"type": "destination",
"lat": 35.758495,
"lng": 51.44255,
"address": "منطقه ۳، داودیه،  میرداماد جنوبی، م مادر ابتدای خ بهروز",
"city": "tehran",
"city_fa": "تهران",
"priority": 1,
"distance": 2830,
"duration": 349,
"coefficient": 1,
"price": 8000
},
{
"type": "destination",
"lat": 35.895452,
"lng": 51.589632,
"address": "بخش رودبارقصران، روستای امامه پایین",
"city": "tehran",
"city_fa": "تهران",
"priority": 2,
"distance": 20192,
"duration": 2492,
"coefficient": 0.42308,
"price": 25500
}
],
"price": 33500,
"credit": true,
"distance": 23022,
"duration": 2841,
"status": "OK",
"user_credit": 996973,
"delay": 0,
"city": "tehran",
"city_fa": "تهران",
"transport_type": "motor_taxi",
"has_return": false,
"cashed": false,
"price_with_return": 46500,
"score": 670,
"score_detail": {
"انجام درخواست": 335,
"اعتباری": 335
},
"final_price": 33500,
"discount": 0,
"discount_coupons": [],
"invalid_discount_coupons": [],
"failed_final_price": 0,
"failed_discount": 0,
"failed_discount_coupons": [],
"scheduled": false
}
}
```

<div class="box-end">
</div>

## سرویس قیمت دسته ای

این سرویس همانند سرویس قیمت عادی است با این تفاوت که شما می توانید تا ۱۵ جفت از ساختار قیمت عادی را در یک درخواست محاسبه کنید.
* شناسه سرویس: 43112
* پارامترهای ورودی:
	* body: یک json با ساختار و پارامترهای زیر:
	*
|     پارامتر               	|     پیش فرض    	|     ضروری    	|     شرح                                                                                                                                                                                                                             	|
|---------------------------	|----------------	|--------------	|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|     transport_type        	|     NULL       	|     true     	|     نوع حمل و نقل سفارش. در حال حاضر مقادیر معتبر برای این ویژگی   عبارتند از: motorbike برای تحویل بسته های ساده ، motor_taxi برای   حمل و نقل مسافر ، cargo برای محموله ، cargo_s برای محموله های کوچک ، و car برای حمل و نقل.    	|
|     addresses[0][type]    	|     NULL       	|     true     	|     باید از نوع origin باشد                                                                                                                                                                                                         	|
|     addresses[0][lat]     	|     NULL       	|     true     	|     عرض از origin آدرس                                                                                                                                                                                                              	|
|     addresses[0][lng]     	|     NULL       	|     true     	|     طول از مبدا آدرس                                                                                                                                                                                                                	|
|     addresses[1][type]    	|     NULL       	|     true     	|     باید از نوع destination باشد                                                                                                                                                                                                    	|
|     addresses[1][lat]     	|     NULL       	|     true     	|     عرض جغرافیایی آدرس destination اول.                                                                                                                                                                                             	|
|     addresses[1][lng]     	|     NULL       	|     true     	|     طول جغرافیایی آدرس destination اول.                                                                                                                                                                                             	|
|     has_return            	|     false      	|     false    	|     اگر تمایل به نحاسبه سفارشی دارید که گزینه return دارد این مقدار را true تنظیم کنید                                                                                                                                              	|
|     cashed                	|     false      	|     false    	|     اگر تمایل دارید نوع پرداخت ضرورتا نقدی باشد این مقدار را true تنظیم کنید.                                                                                                                                                       	|

*  نمونه درخواست ارسالی:

```javascript
[
{
"transport_type":"car",
"addresses":[
{
"type":"origin",
"lat":35.75678,
"lng":51.411255
},
{
"type":"destination",
"lat":35.758495,
"lng":51.44255
},
"has_return":false,
"cashed":false
},
{
"transport_type":"motor_taxi",
"addresses":[
{
"type":"origin",
"lat":35.75678,
"lng":51.411255
},
{
"type":"destination",
"lat":35.895452,
"lng":51.589632
}
],
"has_return":false,
"cashed":false
}
]
```
* اسخ برگشتی: یک json با ساختار و پارامترهای زیر:

|     پارامتر              	|     توضیحات                                                                                                                                                                                                                           	|
|--------------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|     status               	|     نشان می دهد که پیشرفت محاسبه موفقیت آمیز بوده یا خیر.                                                                                                                                                                             	|
|     price                	|     قیمت محاسبه شده کل.                                                                                                                                                                                                               	|
|     credit               	|     نوع پرداخت سفارش را نشان می دهد (پرداخت با اعتبار یا پول نقد).   فقط درصورتی که اعتبار کافی در حساب خود برای آن سفارش داشته باشید صادق خواهد   بود. در صورت کمبود اعتبار یا اینکه cashed=true باشد این ویژگی false   خواهد بود    	|
|     distance             	|     تخمین فاصله بین منبع و مقصد                                                                                                                                                                                                       	|
|     duration             	|     مدت زمان تخمینی از مسیر بین مبدا و مقصد                                                                                                                                                                                           	|
|     user_credit          	|     اعتبار فعلی شما (به تومان).                                                                                                                                                                                                       	|
|     price_with_return    	|     قیمت محاسبه شده برای سفارش ، در صورتیکه has_return   = true   باشد                                                                                                                                                                	|

<div class="box-end">
</div>

## سفارشات
### جزئیات رسیدگی به سفارش
در ادامه مراحل محتلف برای تکمیل سفارش در دسترس است.
1- ایجاد سفارش: در ابتدا وضعیت سفارش new  است  که بیانگر این موضوع است که سفارش به تازگی ایجاد شده است. سفارش حداقل باید دو آدرس داشته باشد. آدرس اول همیشه از نوع origin و دومی از نوع destination است. اگر سفارش شامل گزینه has return باشد، آخرین آدرس سفارش از نوع return خواهد بود اما هیچ فرقی با آدرس origin  یا destination نخواهد داشت. سفارشات می توانند چندین آدرس destination داشته باشند که در حال حاضر محدود به 5 آدرس هستند. در این مرحله هر آدرس در وضعیت pending قرار خواهد گرفت. در این مرحله سفارش می تواند توسط شما لغو شود برای کسب اطلاعات بیشتر در مورد لغو سفارش، به مرحله بعدی مراجعه کنید.

2- اکنون زمان آن رسیده است که سفارش را شروع کنیم. در این مرحله، سفارش به وضعیت searching می رسد، این بدان معنی است که ما در بین پیک های موجود که به آدرس اصلی که در لیست آدرس ها قرار دارد نزدیکترین گزینه را جستجو می کنیم. علامت زمانی که در آن فرآیند اعزام آغاز شده است به عنوان ویژگی launched_at  در مورد سفارش تنظیم می شود. اگر هیچ پیکی برای سفارش پیدا نشود، یا هیچ پیکی سفارش را نپذیرد دستگاه ارسال کننده پس از 10 دقیقه جستجو را متوقف می کند و وضعیت سفارش را به expired به روزرسانی می کند. شما می توانید سفارش را تا این مرحله لغو کنید.  پس از لغو، وضعیت به cancelled تغییر می یابد و ویژگی cancelled_by  که حاوی id شما است تنظیم می شود.  در هر دو حالت انقضا و انصراف ، ویژگی stopped_at  دقیقاً به ما می­گوید که پیشرفت کی متوقف شده است.

3- پذیرش سفارش:  هنگامی که یک سفارش توسط یکی از پیکهای ما پذیرفته می شود وضعیت سفارش به accepted  تغییر خواهد کرد و ویژگی accepted_at  توسط علامت زمانی زمان قبول سفارش پر خواهد شد. ویژگی های duration و distance آدرس اول (آدرس origin) براساس فاصله و مدت زمان محاسبه شده بر اساس موقعیت پیک که در آن سفارش را پذیرفته است ، تعیین می شود. شما همچنان می توانید سفارش را بعد از این مرحله لغو کنید. از این پس ، سایر اقدامات روی آدرس ها تأثیر می گذارد.  اقدامات در آدرس اول سفارش (آدرس origin) ، بر مقادیر ترتیب ، تغییر status ، picking_atو delivering_at  تأثیر می گذارد.  آدرسهای دیگر به جز آخرین مورد ، تاثیری در سفارش ندارند. آخرین آدرس delivered_at  و همچنین ویژگی های `status`  زمانی که چه زمانی و با چه ترتیبی سفارش تحویل داده شده  را پر می کند

4- رسیدن به مبدأ: در این مرحله وضعیت آدرس origin به arrived تغییر خواهد کرد و ویژگی arrived_at  با زمان رسیدن پیک پر خواهد شد همچنین وضعیت سفارش به picking  تغییر می کند و ویژگی picking_at با مقدار arrived_at پر می شود. در این مرحله پیک قادر خواهد بود بعد از 5 دقیقه سفارش را در صورت عدم مشاهده پیشرفت reject کند و یا با توافق با شما سفارش را لغو کند. در این حالت وضعیت سفارش به cancelled  تغییر خواهد کرد و ویژگی cancelled_by  به id پیک مسئول تغییر می یابد ، همچنین topped_at  با زمان لغو سفارش پر می شود.

5- رسیدگی به آدرس مبدا: وضعیت آدرس origin به handled  تغییر خواهد کرد و ویژگی handled_at  با زمان رسیدگی به آدرس و همچنین وضعیت سفارش به delivering  تغییر داده خواهد شد و ویژگی delivering_at  با مقدار`handled_at`  پر خواهد شد.

6- رسیدن به آدرس بعدی: وضعیت آدرس بعدی که معمولاً یک آدرس destination است، اما اگر نیاز به بازگشت پیک به آدرس اول باشد می تواند یک آدرس return نیز باشد، به handled  تغییر خواهد کرد و ویژگی handled_at با زمان رسیدن پر خواهد شد. توجه داشته باشید که اطلاعات سفارش در این مرحله در دسترس نخواهد بود.

7- رسیدگی به آدرس بعدی: وضعیت آدرس بعدی که مجددا معمولا یک آدرس destination است، اما اگر نیاز به بازگشت پیک به آدرس اول باشد می تواند یک آدرس return نیز باشد، به handled  تغییر خواهد کرد و ویژگی handled_at با زمان رسیدگی به آدرس پر خواهد شد. اگر این آخرین آدرس باشد، در صورتی که گزینه بازگشت برای سفارش وجود داشته باشد نوع آدرس return خواهد بود در غیر این صورت این آدرس نیز از نوع destination خواهد بود. اکنون وضعیت سفارش به delivered  تغییر خواهد کرد و ویژگی delivered_at  با مقدار handled_at  پر خواهد شد.

8- اتمام سفارش. وضعیت سفارش به finished  تغییر خواهد کرد و ویژگی finished_atبا علامت زمانی اتمام سفارش پر خواهد شد

<div class="box-end">
</div>

## سرویس ایجاد سفارش

هنگامی که قیمت سفارش خود را محاسبه کردید، می توانید با استفاده از این سرویس برای ایجاد سفارش جدید استفاده کنید.
* شناسه سرویس: 43148
* پارامترهای ورودی:
	* body: یک json با ساختار و پارامترهای زیر:

|     پارامتر                                	|     پیش فرض    	|     ضروری    	|     توضیحات                                                                                                                                                                                                                         	|
|--------------------------------------------	|----------------	|--------------	|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|     transport_type                         	|     NULL       	|     true     	|     نوع حمل و نقل سفارش. در حال حاضر مقادیر معتبر برای این ویژگی   عبارتند از: motorbike برای تحویل بسته های ساده ، motor_taxi برای   حمل و نقل مسافر ، cargo برای محموله ، cargo_s برای محموله های کوچک ، و car برای حمل و نقل.    	|
|     addresses[0][type]                     	|     NULL       	|     true     	|     باید از نوع origin باشد                                                                                                                                                                                                         	|
|     addresses[0][lat]                      	|     NULL       	|     true     	|     عرض از origin  آدرس                                                                                                                                                                                                             	|
|     addresses[0][lng]                      	|     NULL       	|     true     	|     طول از origin  آدرس                                                                                                                                                                                                             	|
|     addresses[0][description]              	|     NULL       	|     false    	|     توضیحی از آدرس که باید از نوع متن باشد.                                                                                                                                                                                         	|
|     addresses[0][unit]                     	|     NULL       	|     false    	|     شماره واحد دقیق آدرس.                                                                                                                                                                                                           	|
|     addresses[0][number]                   	|     NULL       	|     false    	|     شماره پلاک دقیق آدرس مقصد.                                                                                                                                                                                                      	|
|     addresses[0][person_fullname]          	|     NULL       	|     false    	|     نام کامل شخصی که بسته را دریافت می کند یا شخصی که در آن آدرس   ساکن است.                                                                                                                                                        	|
|     addresses[0][person_phone]             	|     NULL       	|     false    	|     شماره تلفن شخص دریافت کننده بسته یا شخص مقیم آن آدرس.                                                                                                                                                                           	|
|     addresses[1][type]                     	|     NULL       	|     true     	|     باید از نوع destination باشد.                                                                                                                                                                                                   	|
|     addresses[1][lat]                      	|     NULL       	|     true     	|     عرض جغرافیایی آدرس destination اول.                                                                                                                                                                                             	|
|     addresses[1][lng]                      	|     NULL       	|     true     	|     طول جغرافیایی آدرس destination اول.                                                                                                                                                                                             	|
|     addresses[1][description]              	|     NULL       	|     false    	|     توضیحی از آدرس که باید از نوع متن باشد.                                                                                                                                                                                         	|
|     addresses[1][unit]                     	|     NULL       	|     false    	|     شماره واحد دقیق آدرس.                                                                                                                                                                                                           	|
|     addresses[1][number]                   	|     NULL       	|     false    	|     شماره پلاک دقیق آدرس مقصد.                                                                                                                                                                                                      	|
|     addresses[1][person_fullname]          	|     NULL       	|     false    	|     نام کامل شخصی که بسته را دریافت می کند یا شخصی که در آن آدرس   ساکن است.                                                                                                                                                        	|
|     addresses[1][person_phone]             	|     NULL       	|     false    	|     شماره تلفن شخص دریافت کننده بسته یا شخص مقیم آن آدرس.                                                                                                                                                                           	|
|     addresses[2][type]                     	|     NULL       	|     false    	|     باید destination باشد.                                                                                                                                                                                                          	|
|     addresses[2][lat]                      	|     NULL       	|     false    	|     عرض جغرافیایی آدرسهای destination  اضافی.                                                                                                                                                                                       	|
|     addresses[2][lng]                      	|     NULL       	|     false    	|     طول جغرافیایی آدرسهای destination  اضافی.                                                                                                                                                                                       	|
|     addresses[2][description]              	|     NULL       	|     false    	|     توضیحی از آدرس که باید از نوع متن باشد.                                                                                                                                                                                         	|
|     addresses[2][unit]                     	|     NULL       	|     false    	|     شماره واحد دقیق آدرس.                                                                                                                                                                                                           	|
|     addresses[2][number]                   	|     NULL       	|     false    	|     شماره پلاک دقیق آدرس مقصد.                                                                                                                                                                                                      	|
|     addresses[2][person_fullname]          	|     NULL       	|     false    	|     نام کامل شخصی که بسته را دریافت می کند یا شخصی که در آن آدرس   ساکن است.                                                                                                                                                        	|
|     addresses[2][person_phone]             	|     NULL       	|     false    	|     شماره تلفن شخص دریافت کننده بسته یا شخص مقیم آن آدرس.                                                                                                                                                                           	|
|     has_return                             	|     false      	|     false    	|     برای محاسبه قیمت سفارشی که گزینه return دارد آن را به true تنظیم کنید.                                                                                                                                                          	|
|     delay                                  	|     NULL       	|     false    	|     می توانید مقدار integer را در واحدminutes  اعمال کنید تا زمان توقف در مکان ها اضافه شود. اگر این گزینه را   تنظیم کرده باشید ، نمی توانید آن را کاهش دهید و فقط می توانید مقدار آن را   افزایش دهید.                            	|
|     scheduled_at                           	|     NULL       	|     false    	|     یک علامت زمانی (2020-10-25 18:45) که مشخص می کند شما تمایل به   ایجاد یک سفارش scheduled دارید که در زمان و   تاریخ دلخواهتان اعمال شود                                                                                         	|
|     cashed                                 	|     false      	|     false    	|     اگر تمایل دارید نوع پرداخت ضرورتا نقدی باشد این مقدار را true تنظیم کنید.                                                                                                                                                       	|
|     extra_params                           	|     NULL       	|     false    	|     یک پارامتر JSON که اجازه می دهد پایگاه داده شما با دستورات الوپیک نقشه برداری   شود (مثال: {my_order_id: 3333). این شی در هر تماس Webhook بازگردانده می شود.                                                                    	|

نمونه درخواست ارسالی:
```javascript
{
"transport_type": "motor_taxi",
"addresses": [
{
"type": "origin",
"lat": "35.755460",
"lng": "51.416874",
"description": "some description for origin",
"unit": "unit of origin address",
"number": "number of origin address",
"person_fullname": "sender s name",
"person_phone": "sender s phone"
},
{
"type": "destination",
"lat": "35.758495",
"lng": "51.442550",
"description": "some description for origin",
"unit": "unit of origin address",
"number": "number of origin address",
"person_fullname": "sender s name",
"person_phone": "sender s phone"
},
{
"type": "destination",
"lat": "35.895452",
"lng": "51.589632",
"description": "some description for origin",
"unit": "unit of origin address",
"number": "number of origin address",
"person_fullname": "sender s name",
"person_phone": "sender s phone"
}
],
"has_return": false,
"cashed": false,
"extra_params": "{\"order_id\":45,\"customer_id\":23}"
}
```

* پاسخ برگشتی: یک json با ساختار و پارامترهای زیر:

|     توضیحات                                                                                           	|     پارامتر           	|
|-------------------------------------------------------------------------------------------------------	|-----------------------	|
|     شناسه سفارش                                                                                       	|     id                	|
|     شماره فاکتور سفارش (5 کاراکتر تصادفی).                                                            	|     invoice_number    	|
|     شناسه مشتری.                                                                                      	|     customer_id       	|
|     نشان یکتای سفارش (برای صفحه ردیابی).                                                              	|     order_token       	|
|     وضعیت سفارش. برای مشاهده لیست کامل وضعیت های ممکن به بخشorder statuses مراجعه کنید.               	|     status            	|
|     عرض جغرافیایی مبداء                                                                               	|     accept_lat        	|
|     طول جغرافیایی مبداء                                                                               	|     accept_lng        	|
|     قیمت سفارش                                                                                        	|     price             	|
|     نوع پرداخت سفارش (نقدی یا اعتباری).                                                               	|     credit            	|
|     فاصله تخمینی بین مبدا و مقصد.                                                                     	|     distance          	|
|     مدت زمان برآورد شده برای مسیر بین مبدا و مقصد.                                                    	|     duration          	|
|     پیشرفت فعلی سفارش در مقیاس 0 تا 1.                                                                	|     progress          	|
|     امضاء سفارش. این پارامتر تا وضعیت تحویل داده شده NULL خواهد بود.                                  	|     signature         	|
|     تصویر سفارش (پیوند تصویر صفحه).                                                                   	|     Screenshot        	|
|     هنگامی که سفارش ارسال شود، اگر سفارش scheduled نباشد این   پارامتر همانند created_at خواهد بود    	|     launched_at       	|
|     آخرین علامت زمانی که سفارش به روز شده است.                                                        	|     updated_at        	|
|     علامت زمانی زمان ایجاد سفارش.                                                                     	|     created_at        	|

نمونه پاسخ برگشتی:

```javascript
{
"status": "success",
"message": null,
"object": {
"transport_type": "motor_taxi",
"customer_id": 3635,
"status": "new",
"traffic_congestion_zone": false,
"traffic_odd_even_zone": false,
"launched_at": "2019-01-07T10:50:11+03:30",
"city": "tehran",
"delay": 0,
"price": 33500,
"credit": true,
"cashed": false,
"has_return": false,
"distance": 23022,
"duration": 2841,
"invoice_number": "62RRB3",
"pay_at_dest": false,
"device_id": null,
"weight": 20,
"is_api": true,
"is_vip": false,
"updated_at": "2019-01-07T10:50:11+03:30",
"created_at": "2019-01-07T10:50:11+03:30",
"id": 15474,
"signature": {
"url": "/uploads/order/15474/signature.jpg?var=1546845611"
},
"order_token": "6cfdfdd4615474g8d70ecff8ef7eeg36352e40d79c6",
"nprice": null,
"subsidy": null,
"signed_by": "",
"final_price": 33500,
"score_calc": {
"score": 670,
"score_detail": {
"انجام درخواست": 335,
"اعتباری": 335
}
},
"addresses": [
{
"id": 30376,
"order_id": 15474,
"customer_id": 3635,
"courier_id": null,
"lat": 35.75678,
"lng": 51.411255,
"type": "origin",
"priority": 0,
"city": "tehran",
"status": "pending",
"address": "تهران، منطقه ۳، کاووسیه، خ گاندی، خ بیستم",
"description": "some description for origin",
"unit": "unit of origin address",
"number": "number of origin address",
"person_fullname": "sender s name",
"person_phone": "sender s phone",
"signed_by": null,
"distance": null,
"google_distance": null,
"duration": null,
"google_duration": null,
"arrived_at": null,
"handled_at": null,
"arrive_lat": null,
"arrive_lng": null,
"handle_lat": null,
"handle_lng": null,
"created_at": "2019-01-07T10:50:11+03:30",
"updated_at": "2019-01-07T10:50:11+03:30",
"deleted_at": null,
"signature": null,
"city_fa": "تهران"
},
{
"id": 30377,
"order_id": 15474,
"customer_id": 3635,
"courier_id": null,
"lat": 35.758495,
"lng": 51.44255,
"type": "destination",
"priority": 1,
"city": "tehran",
"status": "pending",
"address": "منطقه ۳، داودیه،  میرداماد جنوبی، م مادر ابتدای خ بهروز",
"description": "some description for destination",
"unit": "unit of destination address",
"number": "number of destination address",
"person_fullname": "receiver s name",
"person_phone": "receiver s phone",
"signed_by": null,
"distance": 2830,
"google_distance": null,
"duration": 349,
"google_duration": null,
"arrived_at": null,
"handled_at": null,
"arrive_lat": null,
"arrive_lng": null,
"handle_lat": null,
"handle_lng": null,
"created_at": "2019-01-07T10:50:11+03:30",
"updated_at": "2019-01-07T10:50:11+03:30",
"deleted_at": null,
"signature": null,
"city_fa": "تهران"
},
{
"id": 30378,
"order_id": 15474,
"customer_id": 3635,
"courier_id": null,
"lat": 35.895452,
"lng": 51.589632,
"type": "destination",
"priority": 2,
"city": "tehran",
"status": "pending",
"address": "بخش رودبارقصران، روستای امامه پایین",
"description": "some description for destination",
"unit": "unit of destination address",
"number": "number of destination address",
"person_fullname": "receiver s name",
"person_phone": "receiver s phone",
"signed_by": null,
"distance": 20192,
"google_distance": null,
"duration": 2492,
"google_duration": null,
"arrived_at": null,
"handled_at": null,
"arrive_lat": null,
"arrive_lng": null,
"handle_lat": null,
"handle_lng": null,
"created_at": "2019-01-07T10:50:11+03:30",
"updated_at": "2019-01-07T10:50:11+03:30",
"deleted_at": null,
"signature": null,
"city_fa": "تهران"
}
],
"order_discount": null,
"extra_param": {
"order_id": 15474,
"params": "{\"order_id\":45,\"customer_id\":23}"
},
"orderDiscount": null
}
}
```

<div class="box-end">
</div>

## سرویس دریافت جزئیات سفارش

برای به دست آوردن جزئیات سفارش از این سرویس استفاده میشود.
* شناسه سرویس: 43306
* پارامترهای ورودی:
	* orderId: شماره سفارش
* پاسخ برگشتی: یک json با ساختار و پارامترهای زیر:

|     توضیحات                                                                                                                                                                                                                                                                                                                    	|     پارامتر                        	|
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|------------------------------------	|
|     شناسه سفارش                                                                                                                                                                                                                                                                                                                	|     id                             	|
|     شماره فاکتور منحصر به فرد سفارش برای مراجع بعدی.                                                                                                                                                                                                                                                                           	|     invoice_number                 	|
|     شناسه شما                                                                                                                                                                                                                                                                                                                  	|     customer_id                    	|
|     شناسه دستگاه مورد استفاده برای ایجاد سفارش.                                                                                                                                                                                                                                                                                	|     device_id                      	|
|     نشان یکتای سفارش                                                                                                                                                                                                                                                                                                           	|     order_token                    	|
|     وضعیت سفارش. برای مشاهده لیست کامل وضعیت های ممکن به بخشorder statuses مراجعه کنید.                                                                                                                                                                                                                                        	|     status                         	|
|     قیمت سفارش                                                                                                                                                                                                                                                                                                                 	|     price                          	|
|     نوع پرداخت سفارش                                                                                                                                                                                                                                                                                                           	|     credit                         	|
|     نوع پرداخت سفارش                                                                                                                                                                                                                                                                                                           	|     cashed                         	|
|     مشخص می کند که آیا سفارش گزینه بازگشت دارد که نشان می دهد که آیا لازم است   پیک پس از رسیدن به آدرس نهایی به آدرس مبدا بازگردد یا خیر.                                                                                                                                                                                     	|     has_return                     	|
|     مشخص می کند که آیا سفارش باید در آدرس مقصد پرداخت شود یا خیر.                                                                                                                                                                                                                                                              	|     pay_at_dest                    	|
|     فاصله تخمینی بین مبدا و مقصد.                                                                                                                                                                                                                                                                                              	|     distance                       	|
|     مدت زمان برآورد شده برای مسیر بین مبدا و مقصد.                                                                                                                                                                                                                                                                             	|     duration                       	|
|     عرض حغرافیایی موقعیتی که پیک سفارش را پذیرفته است.                                                                                                                                                                                                                                                                         	|     accept_lat                     	|
|     طول جغرافیایی موقعیتی که پیک سفارش را پذیرفته است.                                                                                                                                                                                                                                                                         	|     accept_lng                     	|
|     مدت زمان تخمین زده شده برای مسیر بین مبداء و موقعیتی که پیک سفارش را پذیرفته   است.                                                                                                                                                                                                                                        	|     accept_duration                	|
|     امتیازی که شما پس از پایان سفارش به پیک می دهید.                                                                                                                                                                                                                                                                           	|     rate                           	|
|     نظر شما در مورد سفارش که می تواند هنگامی که شما سفارش را finish یا cancel می کنید یا در صورت لغو سفارش توسط تیم   پشتیبانی پر شود                                                                                                                                                                                          	|     comment                        	|
|     پیشرفت فعلی سفارش در مقیاس 0 تا 1.                                                                                                                                                                                                                                                                                         	|     progress                       	|
|     امضاء سفارش. این پارامتر تا وضعیت تحویل داده شده NULL خواهد بود.                                                                                                                                                                                                                                                           	|     signature                      	|
|     تصویر پیشرفت سفارش در نقشه.                                                                                                                                                                                                                                                                                                	|     Screenshot                     	|
|     هنگامی که سفارش ارسال شود، اگر سفارش scheduled نباشد این   پارامتر همانند created_at خواهد بود                                                                                                                                                                                                                             	|     launched_at                    	|
|     آخرین علامت زمانی که سفارش به روز شده است.                                                                                                                                                                                                                                                                                 	|     updated_at                     	|
|     علامت زمانی زمان ایجاد سفارش.                                                                                                                                                                                                                                                                                              	|     created_at                     	|
|     این پارامتر شامل اطلاعات پیکی است که سفارش را پذیرفته است. شامل phone ، firstname ، lastname، avatar، abs_avatar. در این پارامتر کلید avatar یک مسیر نسبی به آواتار شماست و abs_avatar مسیر مطلق است. توجه داشته باشید {user_id} در URL با شناسه پیک   یا مشتری بسته به اینکه پارامتر متعلق به کدام است جایگزین می شود.    	|     courier                        	|
|     این پارامتر کاربری شماست                                                                                                                                                                                                                                                                                                   	|     customer                       	|
|     نسخه خلاصه آخرین موقعیت ضبط شده پیکی که سفارش را قبول کرده. این نسخه شامل   شماره سفارشبه عنوان id، شناسه پیک   به عنوان courier_id آخرین عرض و طول جغرافیایی ضبط شده پیک به عنوان lat  و lng و درنهایت updated_at  به عنوان آخرین علامت   ن زمانی که این پارامترتغییراتی را ثبت کرده است.                                 	|     last_position_minimal          	|

نمونه پاسخ برگشتی:

```javascript
{
"status": "success",
"message": null,
"object": {
"id": 15474,
"invoice_number": "62RRB3",
"customer_id": 3635,
"device_id": null,
"courier_id": 3840,
"cancelled_by": null,
"status": "delivered",
"distance": 23022,
"duration": 2841,
"price": 33500,
"credit": true,
"cashed": false,
"has_return": false,
"pay_at_dest": false,
"delay": 0,
"is_vip": 0,
"transport_type": "motor_taxi",
"city": "tehran",
"is_api": true,
"weight": 20,
"traffic_odd_even_zone": 0,
"traffic_congestion_zone": 0,
"accept_lat": 35.755292742349,
"accept_lng": 51.415393095455,
"rate": 0,
"comment": null,
"scheduled_at": null,
"launched_at": "2019-01-07T10:50:11+03:30",
"accepted_at": "2019-01-07T10:50:18+03:30",
"delivered_at": "2019-01-07T10:52:08+03:30",
"finished_at": null,
"stopped_at": null,
"removed_at": null,
"created_at": "2019-01-07T10:50:11+03:30",
"updated_at": "2019-01-07T10:52:08+03:30",
"deleted_at": null,
"picking_at": "2019-01-07T10:50:37+03:30",
"delivering_at": "2019-01-07T10:50:55+03:30",
"screenshot": {
"url": "https://sandbox-api.alopeyk.com/api/v2/screenshots?markers=origin,35.75678,51.411255|destination,35.758495,51.44255|destination,35.895452,51.589632"
},
"addresses": [
{
"lat": "35.75678",
"lng": "51.411255",
"type": "origin",
"priority": 0,
"arrived_at": "2019-01-07T10:50:37+03:30",
"handled_at": "2019-01-07T10:50:55+03:30",
"id": 30376,
"city": "tehran",
"order_id": "15474",
"customer_id": "3635",
"courier_id": "3840",
"status": "handled",
"address": "تهران، منطقه ۳، کاووسیه، خ گاندی، خ بیستم",
"description": "some description for origin",
"unit": "unit of origin address",
"number": "number of origin address",
"person_fullname": "sender s name",
"person_phone": "sender s phone",
"signed_by": "",
"distance": "408",
"duration": "50",
"created_at": "2019-01-07T10:50:11+03:30",
"updated_at": "2019-01-07T10:50:55+03:30",
"deleted_at": "",
"arrive_lat": "35.755289373482185",
"arrive_lng": "51.41540617273421",
"handle_lat": "35.75528975658215",
"handle_lng": "51.41541251821029",
"signature": {
"url": "/uploads/order/15474/address/30376/signature.jpg?var=1546846129"
},
"city_fa": "تهران"
},
{
"lat": "35.758495",
"lng": "51.44255",
"type": "destination",
"priority": 1,
"arrived_at": "2019-01-07T10:51:13+03:30",
"handled_at": "2019-01-07T10:51:32+03:30",
"id": 30377,
"city": "tehran",
"order_id": "15474",
"customer_id": "3635",
"courier_id": "3840",
"status": "handled",
"address": "منطقه ۳، داودیه،  میرداماد جنوبی، م مادر ابتدای خ بهروز",
"description": "some description for destination",
"unit": "unit of destination address",
"number": "number of destination address",
"person_fullname": "receiver s name",
"person_phone": "receiver s phone",
"signed_by": "",
"distance": "2830",
"duration": "349",
"created_at": "2019-01-07T10:50:11+03:30",
"updated_at": "2019-01-07T10:51:32+03:30",
"deleted_at": "",
"arrive_lat": "35.75529166468492",
"arrive_lng": "51.415383898653836",
"handle_lat": "35.7552837694252",
"handle_lng": "51.4153970328592",
"signature": {
"url": "/uploads/order/15474/address/30377/signature.jpg?var=1546846129"
},
"city_fa": "تهران"
},
{
"lat": "35.895452",
"lng": "51.589632",
"type": "destination",
"priority": 2,
"arrived_at": "2019-01-07T10:51:50+03:30",
"handled_at": "2019-01-07T10:52:08+03:30",
"id": 30378,
"city": "tehran",
"order_id": "15474",
"customer_id": "3635",
"courier_id": "3840",
"status": "handled",
"address": "بخش رودبارقصران، روستای امامه پایین",
"description": "some description for destination",
"unit": "unit of destination address",
"number": "number of destination address",
"person_fullname": "receiver s name",
"person_phone": "receiver s phone",
"signed_by": "",
"distance": "20192",
"duration": "2492",
"created_at": "2019-01-07T10:50:11+03:30",
"updated_at": "2019-01-07T10:52:08+03:30",
"deleted_at": "",
"arrive_lat": "35.755292797575216",
"arrive_lng": "51.41538377459997",
"handle_lat": "35.755293345216415",
"handle_lng": "51.41536923741546",
"signature": {
"url": "/uploads/order/15474/address/30378/signature.jpg?var=1546846129"
},
"city_fa": "تهران"
}
],
"eta_minimal": {
"id": 636,
"last_position_id": 1814,
"duration": 4396,
"distance": 45694,
"action": "handle",
"address_id": "30378",
"updated_at": "2019-01-07 10:51:34"
},
"courier_info": {
"id": 3840,
"phone": "09493273305",
"firstname": "محمد رضا",
"lastname": "نورشی",
"email": "",
"referral_code": "A36A1",
"plate_number": "",
"rates_avg": "0.0000",
"avatar": {
"url": "/uploads/user/3840/avatar.jpg?var=1546846129"
},
"abs_avatar": {
"url": "https://api.alopeyk.com/uploads/user/3840/avatar.jpg?var=1546846129"
},
"last_online": null,
"is_online": null
},
"launched_or_created_at": "2019-01-07T10:50:11+03:30",
"progress": "1.0000",
"last_position_minimal": null,
"addresses_timeline": [
{
"id": 30376,
"priority": 0,
"status": "handled",
"type": "origin",
"signature": null,
"city_fa": null
},
{
"id": 30377,
"priority": 1,
"status": "handled",
"type": "destination",
"signature": null,
"city_fa": null
},
{
"id": 30378,
"priority": 2,
"status": "handled",
"type": "destination",
"signature": null,
"city_fa": null
}
],
"next_address_any_full": null,
"signature": {
"url": "/uploads/order/15474/address/30378/signature.jpg?var=1546846129"
},
"order_token": "6cfdfdd4615474g8d70ecff8ef7eeg36352e40d79c6",
"nprice": null,
"subsidy": null,
"signed_by": "",
"final_price": 33500,
"score_calc": {
"score": 670,
"score_detail": {
"انجام درخواست": 335,
"اعتباری": 335
}
},
"order_discount": null,
"extra_param": {
"order_id": 15474,
"params": "{\"order_id\":45,\"customer_id\":23}"
},
"courier_vehicle": null,
"orderDiscount": null,
"customerScore": 670,
"courierVehicle": null
}
}
```
<div class="box-end">
</div>

## سرویس لغو سفارش

با استفاده از این سرویس، قبل از رسیدن پیک می توانید هر سفارشی را لغو کنید (قبل از وضعیت پذیرفته شده).
* شناسه سرویس: 43308
* پارامترهای ورودی:
	* orderId: شماره سفارش
* نمونه پاسخ برگشتی:

```javascript
{
"status": "success",
"message": null,
"object": {
"id": 14757,
"status": "cancelled",
"courier_id": 3136,
"customer_id": 86,
"signature": {
"url": "/uploads/order/14757/signature.jpg?var=1540380369"
},
"order_token": null,
"nprice": null,
"subsidy": null,
"signed_by": "",
"final_price": null
}
}
```

<div class="box-end">
</div>

## مقادیر وضعیت سفارش

در API الوپیک وضعیت سفارش (status) می تواند مقادیر زیر را داشته باشد:

|     شرح                                                                                                                                                                                                                   	|     وضعیت         	|
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|-------------------	|
|     سفارش ایجاد شده است و آماده ارسال به نزدیکترین پیک موجود است.                                                                                                                                                         	|     new           	|
|     دستگاه ارسال کننده در حال حاضر به دنبال پیک های موجود در نزدیکی است و   منتظر است تا آنها سفارش را بپذیرند.                                                                                                           	|     searching     	|
|     سفارش لغو شده است. اگر این   اتفاق توسط مشتری روی دهد باید قبل از وضعیت picking باشد در غیر   این صورت به این معنی است که تیم پشتیبانی سفارش را لغو کرده است.                                                         	|     cancelled     	|
|     پیک موجود برای سفارش یافت نشد یا هیچ پیکی درخواست شما را پاسخ نداده است یا   قبول نکرده است                                                                                                                           	|     Expired       	|
|     یکی از پیکهای ما این سفارش را پذیرفته است.                                                                                                                                                                            	|     accepted      	|
|     پیک به مبداء سفارش رسیده است که در واقع آدرس اول (origin) است.                                                                                                                                                        	|     picking       	|
|     یک با موفقیت آدرس اول را اداره کرده است و اکنون مشعول تحویل دادن بسته   (ها) است                                                                                                                                      	|     delivering    	|
|     پیک با موفقیت همه بسته ها را در آدرس های تعیین شده خود تحویل داده بدین   معنی که پیک آدرس ها را handled کرده.                                                                                                         	|     Delivered     	|
|     این وضعیت ضروزی نیست. شما می توانید سفارش را تمام کرده و پیک ما را ارزیابی   کنید.در این حالت ضمن به روز کردن سفارش به این وضعیت ، پارامترهای rate و comment توسط شما پر می شوند.                                     	|     finished      	|
|     این وضعیت مختص سفارشات scheduled است. پس از رسیدن به علامت زمانی scheduled_at سفارش بصورت خودکار ارسال می شود و status آن به new به روز می   شود. از این مرحله سفارشات همان روال ذکر شده در بالا را دنبال می کنند.    	|     scheduled     	|

<div class="box-end">
</div>

## سرویس ویرایش سفارش

برای ویرایش و بروزرسانی سفارشات، نوع حمل و نقل یک گروه خاص را می توان به نوعی دیگر از همان گروه تغییر داد. بدان معنی که انواع حمل و نقل سفارشات موتور را نمی توان به انواع حمل و نقل متعلق به گروه خودرو یا باری تغییر داد.
* گروه موتور: motorbike و motor_taxi
* گروه ماشین: car و car_taxi
* گروه محموله: cargo و cargo_s

اگر سفارش دارای برگشت باشد و پیک سفر را در مسیر برگشت به مبداء آغاز کرده باشد پارامتر has_return قابل حذف نیست. به منظور ویرایش جزئیات سفارش، می توان این سرویس را فراخوانی کرد.
* شناسه سرویس: 43310
* پارامترهای ورودی:
	* orderId: شماره سفارش
	* body:  یک json با ساختار و پارامترهای زیر:

|     پارامتر                  	|     پیش فرض    	|     ضروری    	|     شرح                                                                                                                                                                                                          	|
|------------------------------	|----------------	|--------------	|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|     has_return               	|     NULL       	|     false    	|     اگر لازم است سفارش شما به origin بازگردد، می­توانید قبل از اینکه پیک به انتهای سفارش برسد این   مقدار را روی true تنظیم کنید                                                                                 	|
|     Cashed و credit          	|     NULL       	|     false    	|     اگر می خواهید payment   type را تغییر دهید، می توانید از این دو گزینه استفاده کنید.     یکی از این دو گزینه باید همیشه true باشد و دیگری false.                                                              	|
|     pay_at_dest              	|     NULL       	|     false    	|     اگر گزینه cashed در حالت true باشد، با تنظیم این گزینه روی true ، می توان هزینه سفارش را در مقصد پرداخت کرد. این   گزینه فقط برای single-destination موجود است.                                              	|
|     delay                    	|     NULL       	|     false    	|     شما می توانید مقدار integer را در واحد   minutes برای اضافه کردن زمان توقف در مکان ها اعمال کنید. اگر این   پارامتر را تنظیک مرده باشد قادر به کاهش آن نیستید و تنها می توانید مقدار آن   را افزایش دهید     	|
|     transport_type           	|     NULL       	|     false    	|     بسته به بخش گروه ها در توضیحات فوق، می­توانید این گزینه را برای تغییر نوع سفر تغییر دهید
                                                                                                                	|
نمونه json ارسالی:

```javascript
{
"has_return": false,
"cashed": false,
"credit": true,
"pay_at_dest": false,
"delay": 20,
"transport_type": "motorbike"
}
```
* پاسخ برگشتی: پاسخ این سرویس ساختاری مانند پاسخ سرویس "دریافت جزییات سفارش" دارد.

<div class="box-end">
</div>

## خطا ها

API های الوپیک از خطاهای زیر استفاده می­کند:

|     مفهوم                                                                                         	|     کد خطا    	|
|---------------------------------------------------------------------------------------------------	|---------------	|
|     درخواست بد - درخواست شما نامعتبر است.                                                         	|     400       	|
|     غیرمجاز - نشانه JWT شما نامعتبر   است.                                                        	|     401       	|
|     ممنوع - شما برای انجام این کار مجوز کافی ندارید.                                              	|     403       	|
|     یافت نشد - منبع مشخص شده یافت نشد.                                                            	|     404       	|
|     روش مجاز نیست- شما با یک متد REST غیر معتبر برای دسترسی به API endpoint تلاش کرده   اید       	|     405       	|
|     قابل قبول نیست- شما با فرمتی که JSON نیست درخواست ارسال کرده اید                              	|     406       	|
|     رفته- منبع درخواستی از سرورهای ما حذف شده است.                                                	|     410       	|
|     درخواست های بسیار زیاد - شما درخواست منابع بسیار زیادی دارید.                                 	|     429       	|
|     خطای داخلی سرور - با سرور خود مشکلی داشتیم. بعدا دوباره تلاش کنید.                            	|     500       	|
|     Bad Gateway - سروربرای لحظاتی نمی تواند درخواست شما را   انجام دهد. بعدا دوباره تلاش کنید.    	|     502       	|
|     سرویس در دسترس نیست - ما برای نگهداری موقتاً آفلاین هستیم. لطفا بعدا   دوباره امتحان کنید.     	|     503       	|

<div class="box-end">
</div>
