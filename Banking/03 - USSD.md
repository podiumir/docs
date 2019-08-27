
# USSD
کد USSD یکی از خدمات ارزش افزوده‌ی پلتفرم پاد است. این سرویس یکی از رایج‌ترین راه‌ها برای پرداخت‌های خرد مردم است. با استفاده از این سرویس کاربران می‌توانند از تمامی مکان‌هایی که تلفن ‌همراه در آن‌جا آنتن دهد، به آسانی پرداخت‌های مرتبط با برنامه‌ی شما را انجام دهند.

<div class="box-end">
</div>


## ثبت امکان تسویه حساب خودکار


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | currencyCode
    
    string
    
    (query)      | کد ارز                                                                                                                |
    | wallet
    
    string
    
    (query)            | کد کیف پول                                                                                                            |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |`...`

<div class="box-end">
</div>

## ثبت امکان تسویه حساب خودکار

    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | guildId *
    
    string
    
    (query)         |
    | currencyCode
    
    string
    
    (query)      | کد ارز                                                                                                                |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## انصراف از درخواست مجوز برداشت مستقیم


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## دریافت گزارش صورت حساب

    | ستون
    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | dateFrom
    
    string
    
    (query)          | حد پایین تاریخ صورتحساب                                                                                               |
    | dateTo
    
    string
    
    (query)            | حد بالای تاریخ صورتحساب                                                                                               |
    | description
    
    string
    
    (query)       | فیلتر روی توضیحات بند سند به صورت Like                                                                                |
    | amountFrom
    
    string
    
    (query)        | حد پایین مبلغ بند                                                                                                     |
    | amountTo
    
    string
    
    (query)          | حد بالای مبلغ بند                                                                                                     |
    | currencyCode
    
    string
    
    (query)      | کد ارز                                                                                                                |
    | debtor
    
    string
    
    (query)            | بدهکار / بستانکار true/false                                                                                          |
    | wallet *
    
    string
    
    (query)          | کد کیف پول                                                                                                            |
    | offset *
    
    string
    
    (query)          | result offset                                                                                                         |
    | size *
    
    string
    
    (query)            | result size                                                                                                           |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## دریافت گزارش صورت حساب


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | dateFrom
    
    string
    
    (query)          | حد پایین تاریخ صورتحساب                                                                                               |
    | dateTo
    
    string
    
    (query)            | حد بالای تاریخ صورتحساب                                                                                               |
    | description
    
    string
    
    (query)       | فیلتر روی توضیحات بند سند به صورت Like                                                                                |
    | amountFrom
    
    string
    
    (query)        | حد پایین مبلغ بند                                                                                                     |
    | amountTo
    
    string
    
    (query)          | حد بالای مبلغ بند                                                                                                     |
    | block
    
    string
    
    (query)             | true/false فیلتر روی حساب های مسدودی یا غیر مسدودی                                                                    |
    | guildId *
    
    string
    
    (query)         | شناسه صنف حساب                                                                                                        |
    | currencyCode
    
    string
    
    (query)      | کد ارز                                                                                                                |
    | debtor
    
    string
    
    (query)            | بدهکار / بستانکار true/false                                                                                          |
    | offset *
    
    string
    
    (query)          | result offset                                                                                                         |
    | size *
    
    string
    
    (query)            | result size                                                                                                           |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## دریافت اعتبار کسب و کار


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | guildId *
    
    string
    
    (query)         | شناسه صنف                                                                                                             |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |
<div class="box-end">
</div>

## میزان اعتبار کاربر رانمایش میدهد.
```
| cellphoneNumber *

string

(query) | شماره موبایل                                                                                                        |
| currencyCode

string

(query)      | کد ارز                                                                                                              |
| wallet

string

(query)            | کد کیف پول                                                                                                          |
| block

string

(query)             | true/false برای موجودی مسدودی true و در غیر اینصورت false ارسال گردد                                                |
| _token_ *

string

(header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود            |
| _token_issuer_ *

string

(header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از s |
```


<div class="box-end">
</div>

## لیست مجوزهای برداشت مستقیم


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | id
    
    string
    
    (query)                | شناسه درخواست                                                                                                         |
    | statusCode
    
    string
    
    (query)        | کد وضعیت درخواست                                                                                                      |
    | fromRequestDate
    
    string
    
    (query)   | تاریخ درخواست شمسی از yyyy/mm/dd                                                                                      |
    | toRequestDate
    
    string
    
    (query)     | تاریخ درخواست شمسی تا yyyy/mm/dd                                                                                      |
    | offset *
    
    string
    
    (query)          | result offset                                                                                                         |
    | size *
    
    string
    
    (query)            | result size                                                                                                           |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## دریافت لیست اصناف کسب و کار


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | offset *
    
    string
    
    (query)          |
    | size *
    
    string
    
    (query)            |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## حذف امکان تسویه حساب خودکار

    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | currencyCode
    
    string
    
    (query)      | کد ارز                                                                                                                |
    | wallet
    
    string
    
    (query)            | کد کیف پول                                                                                                            |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## حذف امکان تسویه حساب خودکار برای کسب و کار


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | guildCode *
    
    string
    
    (query)       |
    | currencyCode
    
    string
    
    (query)      | کد ارز                                                                                                                |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## درخواست مجوز برداشت مستقیم


    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |
<div class="box-end">
</div>

## درخواست برداشت اعتبار

    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | wallet
    
    string
    
    (query)            | کد کیف پول                                                                                                            |
    | amount
    
    string
    
    (query)            | مبلغ برداشت                                                                                                           |
    | currencyCode
    
    string
    
    (query)      | کد ارز                                                                                                                |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |
    | _ott_ *
    
    string
    
    (header)          | one time token - این توکن را در سرویس قبلی دریافت کرده اید.برای دریافت مجدد می توانید سرویس /nzh/ott/ را صدا کنید     |

<div class="box-end">
</div>

## لغو مجوز برداشت مستقیم
 

    | cellphoneNumber *
    
    string
    
    (query) | شماره موبایل                                                                                                          |
    | _token_ *
    
    string
    
    (header)        | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header) | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>

## تایید مجوز برداشت مستقیم
 

    | cellphoneNumber *
    
    string
    
    (query)    | شماره موبایل                                                                                                          |
    | otp
    
    string
    
    (query)                  | otp                                                                                                                   |
    | selectedDepositIndex
    
    string
    
    (query) | ایندکس سپرده                                                                                                          |
    | _token_ *
    
    string
    
    (header)           | توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود              |
    | _token_issuer_ *
    
    string
    
    (header)    | مرجع صادرکننده توکن و می توان به عنوان پارامتر هم وارد نمود.0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso |

<div class="box-end">
</div>
