- [مقدمه](#menu)
- [پیش از شروع](#menu)
- [دریافت توکن](#menu)
- [استعلام نمره منفی گواهینامه](#menu)
- [استعلام کارت خودرو](#menu)
- [استعلام گواهینامه](#menu)
- [جداول](#menu)
- [خطاها](#menu)

## مقدمه
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
|   Authorization    |     دریافتی از سرویس دریافت توکن    |

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

## دریافت توکن

برای استفاده از تمامی سرویس ها می بایست ابتدا با استفاده از این سرویس توکن را دریافت نموده و در پارامتر Authorization در هدر درخواست ارسال کنید.
* شناسه سرویس: 46742
* پارامترهای ورودی: ندارد.
* پاسخ برگشتی: Json با پارامترهای زیر:

| پارامتر | نوع | توضیحات |
|--------:|---------:|---------:|
| \_token_type\_ | String | نوع توکن |
| \_access_token\_ | String | توکن دسترسی |

توجه : فرمت ارسال توکن در پارامتر Authorization به صورت زیر است:  

Authorization: [token_type] [access_token]  

## استعلام نمره منفی گواهینامه

با استفاده از این سرویس میتوان نمره منفی یک گواهینامه را استعلام نمود.
* شناسه سرویس: 44094
* پارامترهای ورودی: یک json با ساختار و پارامترهای زیر:

| توضیحات | نام پارامتر |
|-----------------:|---------------:|
| شماره گواهینامه | LicenseNumber |

* پاسخ برگشتی:
در صورت استعلام موفق فیلدهای خروجی به صورت Json:

| مقدار | پارامتر |
|-----------------------------------------------------------------|---------|
| کد | Status |
| پیام | Message |
| شامل:<br>NegativeScore : نمره منفی<br>OffenseCount : تعداد تخلف | Data |

در غیر اینصورت :

| مقدار | پارامتر |
|--------------------------------:|---------:|
|  کد خطا | Status |
| پیام خطا | Message |

<div class="box-end">
</div>

## استعلام کارت خودرو


با استفاده از این سرویس میتوان اطلاعات کارت خودرو را استعلام نمود.
* شناسه سرویس: 44095
* پارامترهای ورودی: یک json با ساختار و پارامترهای زیر:

| توضیحات | نام پارامتر |
|-----------------------------------------------------------------------------:|-------------:|
| شماره پلاک (به صورت عدد 9 رقمی) به کمک جدول 2<br>نمونه: 120636567=67-345ج12 | PlateNumber |

* پاسخ برگشتی:
در صورت استعلام موفق فیلدهای خروجی به صورت Json:

| مقدار | پارامتر |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------:|---------:|
| کد | Status |
| پیام | Message |
| شامل:<br>CardNumber : شماره پشت کارت خودرو<br>CardType : نوع کارت<br>Date : تاریخ آخرین وضعیت<br>Plate : شماره پلاک<br>PostalBarcode : بارکد پستی<br>Status : وضعیت | Data |

در غیر اینصورت :

| مقدار | پارامتر |
|--------------------------------:|---------:|
|  کد خطا | Status |
| پیام خطا | Message |

<div class="box-end">
</div>

## استعلام گواهینامه

با استفاده از این سرویس میتوان اطلاعات گواهینامه را استعلام نمود.
* شناسه سرویس: 44096
* پارامترهای ورودی: یک json با ساختار و پارامترهای زیر:

| توضیحات | نام پارامتر |
|---------:|-------------:|
| کد ملی | NationalId |

* پاسخ برگشتی:
در صورت استعلام موفق فیلدهای خروجی به صورت Json:

| مقدار | پارامتر |
|------------------------------------------------------------------------------------------------------------:|---------:|
| کد | Status |
| پیام | Message |
| شامل:<br>Barcode : بارکد<br>CardStatus : وضعیت گواهینامه<br>ExportationDate : تاریخ صدور<br>Status : وضعیت | Data |

در غیر اینصورت :

| مقدار | پارامتر |
|--------------------------------:|---------:|
|  کد خطا | Status |
| پیام خطا | Message |

<div class="box-end">
</div>


## جداول

**شرح جزئیات قبوض**

| شرح | پارامتر | نوع قبض |
|-|-|-|
| شماره پرونده | FileNumber | آب |
| نام | OwnerName | آب |
| شهر | City | آب |
| آدرس | Address | آب |
| کد پستی | PostalCode | آب |
| نوع کاربری | AccountType | آب |
| تعداد واحد | UnitsNumber | آب |
| سریال قبض | BillSerial | آب |
| شماره بدنه کنتور | MeterBodyNumber | آب |
| وضعیت کنتور | MeterStatus | آب |
| قطر انشعاب آب | BranchDiameter | آب |
| قطر سیفون | WasteWaterDiameter | آب |
| ظرفیت قراردادی | ContractCapacity | آب |
| تاریخ قبلی | PreviousDate | آب |
| تاریخ فعلی | CurrentDate | آب |
| شماره قبلی | PreviousNumber | آب |
| شماره فعلی | CurrentNumber | آب |
| مصرف دوره | TotalConsumption | آب |
| بدهی گذشته | PreviousDebt | آب |
| میانگین مصرف | AverageConsumption | آب |
| تعداد روز دوره | TotalDay | آب |
| آب بهای مصرفی | WaterPrice | آب |
| تبصره ۲ | Note2 | آب |
| تبصره ۳ | Note3 | آب |
| مالیات بر ارزش افزوده | Tax | آب |
| تکالیف قانون بودجه | VillageAbfaPortion | آب |
| بهای دفع فاضلاب | WasteWaterFee | آب |
| مصرف مازاد | ExtraConsumption | آب |
| تاریخ صدور قبض | BillExportationDate | آب |
| مجموع صورتحساب | TotalBilling | آب |
| کسر هزارریال | DeductionAmount1000Rial | آب |
| روستا | Village | آب |
| منطقه | Area | آب |
| تاریخ صدور | BillExportationDate | برق |
| تاریخ قرائت قبلی | PreviousReadingDate | برق |
| تاریخ عدم قبول | RejectDate | برق |
| تاریخ قرائت فعلی | CurrentReadingDate | برق |
| مصرف میان باری | NormalConsumption | برق |
| مصرف اوج بار | PeakConsumption | برق |
| مصرف کم باری | LowConsumption | برق |
| مصرف روز جمعه | FridayConsumption | برق |
| مصرف راکتیو | ReactiveConsumption | برق |
| تقاضای قرائت | DemandRead | برق |
| میانگین مصرف | AverageConsumption | برق |
| مبلغ قابل پرداخت | BillPayableAmount | برق |
| مبلغ دوره | PeriodAmount | برق |
| مبلغ بیمه | InsuranceAmount | برق |
| مبلغ مالیات (در سهم   ارزش افزوده) | TaxAmount | برق |
| مبلغ عوارض | PaytollAmount | برق |
| مبلغ عوارض برق | ElectricityTaxAmount | برق |
| بدهی پیشین | PreviousDebt | برق |
| مبلغ انرژی | EnergyAmount | برق |
| مبلغ راکتیو | ReactiveAmount | برق |
| مبلغ تقاضا | DemandAmount | برق |
| آبونمان | SubscriptionAmount | برق |
| مبلغ فصل | SeasonAmount | برق |
| مبلغ رایگان | FreeAmount | برق |
| مبلغ تخفیف گاز | GasDiscountAmount | برق |
| مبلغ تخفیف | DiscountAmount | برق |
| تعداد روز گرم | WarmDaysCount | برق |
| تعداد روز سرد | ColdDaysCount | برق |
| تعداد روز | TotalDaysCount | برق |
| نام شرکت توزیع | CompanyName | برق |
| فاز | Phase | برق |
| نوع ولتاژ | VoltageType | برق |
| آمپراژ | Amper | برق |
| قدرت | ContractDemand | برق |
| نوع تعرفه | TariffType | برق |
| نوع مشترک | CustomerType | برق |
| نام مشترک | CustomerName | برق |
| نام خانوادگی مشترک | CustomerFamily | برق |
| آدرس | Address | برق |
| کدپستی | PostalCode | برق |
| مبلغ بدهی مصرف | ConsumptionDebtAmount | برق |
| مبلغ بدهی سایر خدمات | OtherDebtAmount | برق |
| مبلغ بدهی انشعاب | BranchDebtAmount | برق |
| شماره شناسایی | IdentificationNumber | برق |
| شماره پرونده | FileNumber | برق |
| رمز رایانه | ComputerPassword | برق |
| دوره | Period | برق |
| سال | Year | برق |
| نام مشترک | OwnerName | گاز |
| نوع مصرف | UseType | گاز |
| شماره اشتراک | SubscriptionNumber | گاز |
| کد آدرس | AddressCode | گاز |
| شهر | City | گاز |
| کد حوزه | AreaCode | گاز |
| سریال کنتور | MeterSerial | گاز |
| شماره پرونده | FileNumber | گاز |
| تعداد واحد | UnitCount | گاز |
| گروه | Group | گاز |
| ظرفیت | Capacity | گاز |
| تاریخ قرائت پیشین | PreviousReadingDate | گاز |
| تاریخ قرائت فعلی | CurrentReadingDate | گاز |
| رقم شمارشگر پیشین | PreviousCounterDigit | گاز |
| رقم شمارشگر فعلی | CurrentCounterDigit | گاز |
| کارکرد شمارشگر | CounterActivity | گاز |
| مصرف استاندارد | StandardConsumption | گاز |
| بهای گاز مصرفی | GasConsumptionAmount | گاز |
| آبونمان | Subscription | گاز |
| عوارض | Taxes | گاز |
| بیمه | Insurance | گاز |
| بدهی متفرقه | OtherDebt | گاز |
| مانده بدهی | RemainingDebt | گاز |
| مانده صورتحساب قبلی | RemainingPreviousInvoice | گاز |
| تعداد بدهی | DebtCount | گاز |
| شماره سری | SerialNumber | گاز |
| مانده مبلغ هزار ریال | RemainingAmount1000Rial | گاز |
| کسر مبلغ هزار ریال | DeductionAmount1000Rial | گاز |
| عوارض گازرسانی به   روستا | VillageGasTaxes | گاز |
| مهلت پرداخت | PaymentDeadLine | تلفن |
| هزینه بین شهری | InterCityCost | تلفن |
| هزینه شهری | CityCost | تلفن |
| هزینه تلفن همراه | MobileCost | تلفن |
| آبونمان | Subscription | تلفن |
| مالیات | Taxes | تلفن |
| عوارض | Charges | تلفن |
| بدهی | Debt | تلفن |
| وضعیت خط | Status | تلفن |
| تاریخ آغاز صورتحساب | StartBillingDate | تلفن |
| تاریخ پایان صورتحساب | EndBillingDate | تلفن |
| مبلغ قابل پرداخت | TotalBilling | تلفن |
| مبلغ | Amount | خلافی |
| شناسه قبض | BillId | خلافی |
| شهر | City | خلافی |
| تاریخ | Date | خلافی |
| شرح تخلف | DeliveryType | خلافی |
| محل تخلف | Location | خلافی |
| شناسه پرداخت | PayId | خلافی |
| نوع تخلف | Type | خلافی |

** اعداد متناسب با حروف پلاک**

| عدد | حرف |
|-|-|
| ۱ | الف |
| ۲ | ب |
| ۳ | پ |
| ۴ | ت |
| ۵ | ث |
| ۶ | ج |
| ۷ | چ |
| ۸ | ح |
| ۹ | خ |
| ۱۰ | د |
| ۱۱ | ذ |
| ۱۲ | ر |
| ۱۳ | ز |
| ۱۴ | ژ |
| ۱۵ | س |
| ۱۶ | ش |
| ۱۷ | ص |
| ۱۸ | ض |
| ۱۹ | ط |
| ۲۰ | ظ |
| ۲۱ | ع |
| ۲۲ | غ |
| ۲۳ | ف |
| ۲۴ | ق |
| ۲۵ | ک |
| ۲۶ | گ |
| ۲۷ | ل |
| ۲۸ | م |
| ۲۹ | ن |
| ۳۰ | و |
| ۳۱ | ه |
| ۳۲ | ی |
| ۳۴ | D |

<div class="box-end">
</div>

## خطاها

| شرح                                            	| پیام پاسخ                                     	| کد پاسخ 	|
|------------------------------------------------	|-----------------------------------------------	|---------	|
| موفق                                           	| Success                                       	| 0       	|
| اجازه دسترسی ندارید                            	| No Access                                     	| 101     	|
| نوع قبض ارسال نشده است                         	| Bill Type is Empty                            	| 102     	|
| پارامتر استعلام ارسال نشده است                 	| Bill Parameter is Empty                       	| 103     	|
| مقدار ورودی نامعتبر است                        	| Wrong parameter                               	| 104     	|
| قبض پرداخت شده است                             	| Bill Paid                                     	| 105     	|
| قبضی یافت نشد                                  	| No Bill                                       	| 106     	|
| نوع قبض اشتباه است                             	| Bill Wrong Type                               	| 107     	|
| ستعلام فعال نمی باشد                           	| Service Disable                               	| 108     	|
| استعلام مورد نظر برای شما فعال نمی باشد        	| Service Disabled                              	| 109     	|
| استعلام فعال نمی باشد                          	| Service Disabled                              	| 110     	|
| استعلام فعال نمی باشد                          	| Service Disabled                              	| 111     	|
| استعلام فعال نمی باشد                          	| Service Disabled                              	| 112     	|
| آرایه قبوض ارسال نشده است                      	| Bills is Empty                                	| 113     	|
| مقدار آرایه قبوض نامعتبر است                   	| Invalid Bills Data                            	| 114     	|
| نام گروه ارسال نشده  است                       	| Please Enter Group Name                       	| 115     	|
| نوع گروه ارسال نشده است                        	| Please Enter Group Type                       	| 116     	|
| نوع گروه اشتباه است                            	| Wrong Group Type                              	| 117     	|
| شناسه گروه ارسال نشده است                      	| Please Enter Group Id                         	| 118     	|
| شناسه گروه اشتباه است                          	| Wrong gGroup Id                               	| 119     	|
| گروه موجود نیست                                	| Group Not Exists                              	| 120     	|
| نوع پارامتر ارسال نشده است                     	| Empty Parameter Type                          	| 121     	|
| پارامتر ارسال نشده است                         	| Empty Parameter                               	| 122     	|
| پارامتر در گروه موجود است                      	| Parameter Exist In This Group                 	| 123     	|
| شناسه پارامتر ارسال نشده است                   	| Empty Parameter Id                            	| 124     	|
| شناسه پارامتر موجود نیست                       	| Parameter Id Not Exist                        	| 125     	|
| پارامتر موجود نیست                             	| Parameter Not Exists                          	| 126     	|
| خطا در درخواست فعالسازی تلفن                   	| Tel Activation Error                          	| 131     	|
| شماره تلفن ارسال نشده است                      	| TelNumber is Empty                            	| 132     	|
| شماره تلفن نامعتبر است                         	| TelNumber is Wrong                            	| 133     	|
| کد فعالسازی ارسال نشده است                     	| ActivationCode is Empty                       	| 134     	|
| شماره تلفن نیاز به  فعالسازی ندارد             	| This Tel Does Not Require Verification        	| 135     	|
| شماره تلفن ابتدا نیاز به درخواست فعالسازی دارد 	| Tel Request ActivationCode    Required        	| 136     	|
| شماره گواهینامه ارسال نشده است                 	| License Number Is Empty                       	| 301     	|
| شماره گواهینامه نادرست است                     	| License Number Is Invalid                     	| 302     	|
| اطلاعات یافت نشد                               	| Information Not Found                         	| 303     	|
| شماره پلاک ارسال نشده است                      	| Plate Number Is Empty                         	| 304     	|
| شماره پلاک نادرست است                          	| Plate Number Is Invalid                       	| 305     	|
| کد ملی ارسال نشده است                          	| National Id Is Empty                          	| 306     	|
| کد ملی نادرست است                              	| National Id Is Invalid                        	| 307     	|
| توکن نامعتبر است                               	| No HTTP resource was found (401 Unauthorized) 	| 16      	|
