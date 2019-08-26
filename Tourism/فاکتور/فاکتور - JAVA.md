
# فاکتور

## توکن یکبار مصرف

[ابتدا jar فایل مربوطه را دانلود و در پروژه خود قرار دهید.](https://github.com/FanapSoft/pod-java-sdk/tree/master/pod-billing-service-java/Sample%20Code/release)

برای استفاده از برخی از تابع ها که تعداد دفعات اجرای آنها مهم است، لازم است پارامتر ott در به تابع داده شود. این پارامتر در هر درخواست که به سرور ارسال می گردد تغییر می کند و ott جدید در پاسخ درخواست صادر می گردد. برای دریافت این پارامتر از تابع زیر استفاده کنید:

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            OttVo ottVo = new OttVo.Builder(baseInfoVo)
                    .build();
            billingService.ott(ottVo, new OnGetResponseListener<String>() {
                @Override
                public void onResponse(ResultVo<String> result) {
                    System.out.println(result.getOtt());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```

 <div class="box-end">
</div>

## ‌صدور فاکتور توسط کسب و کار

هرگونه پرداخت در پلتفرم پاد، از طریق فاکتور صورت می گیرد. در این بخش صدور فاکتور با استفاده از توکن کسب و کار شرح داده شده و می توان با خروجی حاصل از این متد، کاربر را به راحتی به درگاه پرداخت هدایت نمود. برای صدور فاکتور از سرویس زیر استفاده نمایید.

مقدار api_token را از پنل مدیریت کسب و کار دریافت نمایید.

اگر محصولی که برای آن فاکتور ثبت می کنید در سیستم ثبت شده نیست، ProductId را با مقدار صفر وارد نمایید.

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setOtt(OTT)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        List<ProductInfo> productInfos = new ArrayList<>();
        ProductInfo productInfo = new ProductInfo();
        productInfo
                .setProductId(0L)
                .setPrice(new BigDecimal(1))
                .setQuantity(new BigDecimal(1))
                .setProductDescription("test");
        productInfos.add(productInfo);

        try {
            IssueInvoiceVo issueInvoiceVo = new IssueInvoiceVo.Builder(baseInfoVo)
                    .setProductInfos(productInfos)
//                    .setUserId(123L)
                    .setGuildCode(SAMPLE_GUILD_CODE)
                    .build();
            billingService.issueInvoice(issueInvoiceVo, new OnGetResponseListener<InvoiceSrv>() {
                @Override
                public void onResponse(ResultVo<InvoiceSrv> result) {
                    System.out.println(result.getResult().getId());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


اکثر عملیات مربوط به فاکتور نیاز به ott دارند که میتوانید آن را از آخرین درخواست به پلتفرم یا از طریق تابع زیر دریافت نمایید. فقط دقت نمایید که توکنی که با آن ott می گیرید با توکنی که در درخواست بعدی باید استفاده شود، یکی باشد.

توجه داشته باشید مقدار ott از api_token متفاوت است، مقدار ott را میتوانید از تابع issueInvoice  هم دریافت نمایید و مجددا در سرویس صدور فاکتور فراخوانی نمایید.

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            OttVo ottVo = new OttVo.Builder(baseInfoVo)
                    .build();
            billingService.ott(ottVo, new OnGetResponseListener<String>() {
                @Override
                public void onResponse(ResultVo<String> result) {
                    System.out.println(result.getOtt());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


 <div class="box-end">
</div>

## نمایش پیش فاکتور

در پلتفرم کسب و کار، فاکتورهایی که پرداخت می شوند به صورت سالانه شماره سریال دریافت می نمایند، بنابرین کسب و کار می تواند برای امور مالی خود به آن شماره سریال استناد نماید. در برخی شرایط، ممکن است کسب و کار بخواهد فاکتور تا زمانی که اقدام به پرداخت آن نشده اصلاً ثبت نگردد. بدین منظور با استفاده از دستور زیر می تواند پیش فاکتور را ثبت نماید و با لینک بعدی آن را نمایش دهد. به محض اینکه مشتری، فاکتور را با کیف پول خود پرداخت نماید یا برای پرداخت وارد درگاه بانکی شود، فاکتور ثبت می گردد. در صورتی که مشتری پرداخت را از طریق درگاه لغو نماید یا اشکالی در پرداخت او به وجود آید، فاکتور به صورت خودکار لغو خواهد شد.

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setOtt(OTT)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        List<ProductInfo> productInfos = new ArrayList<>();
        ProductInfo productInfo = new ProductInfo();
        productInfo
                .setProductId(0L)
                .setPrice(new BigDecimal(1))
                .setQuantity(new BigDecimal(1))
                .setProductDescription("test");
        productInfos.add(productInfo);

        try {
            CreatePreInvoiceVo createPreInvoiceVo = new CreatePreInvoiceVo.Builder(baseInfoVo)
                    .setRedirectURL(RIDERECT_URI)
                    .setUserId(513304L)
                    .setProductInfos(productInfos)
                    .setGuildCode(SAMPLE_GUILD_CODE)
                    .build();

            billingService.createPreInvoice(createPreInvoiceVo, new OnGetResponseListener<String>() {
                @Override
                public void onResponse(ResultVo<String> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


 <div class="box-end">
</div>

## دریافت فاکتور

برای مشاهده فاکتورهایی که کسب و کار شما صادر نموده و وضعیت آنها می توانید به پنل مدیریت کسب و کار خود به آدرس https://gw.pod.land مراجعه نمایید و از منوی << مالی ، فاکتورها >> آنها را مشاهده نمایید. این قسمت امکان فیلتر یا جستجو در شرح فاکتورها را نیز دارد.

همچنین می توانید برای استفاده در برنامه خود، از تابع زیر استفاده نمایید تا از پرداخت آن توسط کاربر اطمینان پیدا کنید:

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            GetInvoiceListVo getInvoiceListVo = new GetInvoiceListVo.Builder(baseInfoVo)
                    .setOffset(0L)
                    .setSize(10L)
                    .build();
            billingService.getInvoiceList(getInvoiceListVo, new OnGetResponseListener<List<InvoiceSrv>>() {
                @Override
                public void onResponse(ResultVo<List<InvoiceSrv>> result) {
                    System.out.println(result.getResult().get(0).getId());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


همچنین برای جستجو در متادیتای ثبت شده برای فاکتور می توانید از تابع زیر استفاده نمایید:

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            GetInvoiceListByMetadataVo getInvoiceListByMetadataVo = new GetInvoiceListByMetadataVo.Builder(baseInfoVo)
                    .build();
            billingService.getInvoiceListByMetadata(getInvoiceListByMetadataVo,
                    new OnGetResponseListener<List<InvoiceSrv>>() {
                        @Override
                        public void onResponse(ResultVo<List<InvoiceSrv>> result) {
                            System.out.println(result.getResult().size());
                        }

                        @Override
                        public void onFailed(PodException e) {
                            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                        }
                    });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


در قسمت metaQuery مقادیر درخواستی خود را به فرم json با استفاده از توصیحات [جستجوی متادیتا](https://docs.pod.land/document/Developer-CustomPost-SearchMetadata) ارسال نمایید.

کد خطاهای رایج در سرویس " **دریافت فاکتور**"

| **errorCode** | **دلیل خطا** | **شرح** |
| 21 | client not authenticated | ارسال توکن اشتباه |
| 999 | UNKHOWN | خطای داخلی |

هم‌چنین امکان دریافت لیست فاکتورها در قالب فایل نیز وجود دارد.

در بین پارامترهای ارسالی یکی از پارامترهای lastNRows و یا بازه زمانی اجباری است.

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            GetInvoiceListAsFileVo getInvoiceListAsFileVo = new GetInvoiceListAsFileVo.Builder(baseInfoVo)
                    .setLastNRows(10L)
                    .build();
            billingService.getInvoiceListAsFile(getInvoiceListAsFileVo, new OnGetResponseListener<ExportServiceSrv>() {
                @Override
                public void onResponse(ResultVo<ExportServiceSrv> result) {
                    System.out.println(result.getResult().getId());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


 <div class="box-end">
</div>

## ابطال فاکتور

در صورتی که فاکتور باطل شود، دیگر قابل پرداخت نیست و در صورتی که قبلا پرداخت شده باشد، مبلغ آن به پرداخت کننده برگشت خواهد خورد.

توجه: در صورتی که فاکتور با شرایط safe=true صادر شده باشد، فقط پرداخت کننده می تواند فاکتور را کنسل کند و اگر safe نباشد فقط   issuer  فاکتور مجاز به کنسلی فاکتور می باشد. 

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            CancelInvoiceVo cancelInvoiceVo = new CancelInvoiceVo.Builder(baseInfoVo)
                    .setId(3581653L)
                    .build();
            billingService.cancelInvoice(cancelInvoiceVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


در صورتی که فاکتور مورد نظر تسهیمی است، شناسه ای که باید به این سرویس ارسال گردد، معادل result -> id موجود در خروجی فاکتور تسهیمی می باشد. در این صورت تمام فاکتورهای ثبت شده برای یک تسهیم مرجوع می گردند.

**خطاهای سرویس کنسل نمودن فاکتور** **:**

| **errorCode** | **دلیل خطا** | **شرح** |
| 4 | PERMISSION_DENIED | اگر مجوز برای برگشت زدن فاکتور نداشته باشید این خطا را دریافت می کنید. |
| 21 | client not authenticated | مقدار توکن اشتباه ارسال شده است. |
| 32 | INVOICE_IS_CANCELED | فاکتور کنسل شده است. |
| 45 | BILL_ALREADY_CLOSED | فاکتور بسته شده قابل ابطال نیست. |
| 999 | UNKNOWN | خطای داخلی |

 <div class="box-end">
</div>

## تایید و بستن فاکتور در یک مرحله

با فراخوانی تابع زیر، می‌توانید همزمان تایید و بستن فاکتور را انجام دهید:
<br>

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            VerifyAndCloseInvoiceVo verifyAndCloseInvoiceVo = new VerifyAndCloseInvoiceVo.Builder(baseInfoVo)
                    .setId(3581653L)
                    .build();
            billingService.verifyAndCloseInvoice(verifyAndCloseInvoiceVo, new OnGetResponseListener<InvoiceSrv>() {
                @Override
                public void onResponse(ResultVo<InvoiceSrv> result) {
                    System.out.println(result.getResult().getId());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


هنگام استفاده از این وب سرویس به نکات زیر دقت نمایید:

1. 		مبلغ فاکتور بعد از واریز شاپرک قابل برداشت خواهد بود
2. 		بعد از فراخوانی این سرویس امکان کاهش فاکتور یا لغو فاکتور وجود ندارد
3. 		جهت واریز وجه به مشتری پرداخت کننده فاکتور، لازم است از تابع transferByInvoice استفاده نمایید که شامل کارمزد می باشد.
4. 		بعد از فراخوانی این سرویس وضعیت فاکتور دیگر تغییر نخواهد کرد

 <div class="box-end">
</div>

## بستن فاکتور

فاکتور هایی که بسته شوند دیگر قابل ابطال نیستند. برای اینکه بتوانید مبالغ فروش خود را تسویه نمایید لازم است حتما فاکتورها را ببندید.

چنان چه فاکتورها به صورت **safe=true**  صادر شده باشد و یا فاکتور متعلق به کسب و کار شما نباشد پیغام خطای " **اجازه بستن این فاکتور را ندارید** " دریافت خواهید کرد.

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            CloseInvoiceVo closeInvoiceVo = new CloseInvoiceVo.Builder(baseInfoVo)
                    .setId(3360466L)
                    .build();
            billingService.closeInvoice(closeInvoiceVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


در صورتی که فاکتور مورد نظر تسهیمی است، شناسه ای که باید به این سرویس ارسال گردد، معادل result -> id موجود در خروجی فاکتور تسهیمی می باشد. تا زمانی که فاکتور بسته نشود هیچکدام از ذینفعان قادر به تسویه و برداشت سهم خود نیستند.

**خطای سرویس "بستن فاکتور** **":**

| **errorCode** | **دلیل خطا** | **شرح** |
| 21 | client not authenticated | ارسال مقدار اشتباه برای توکن |
| 45 | BILL_ALREADY_CLOSED | فاکتور بسته شده است. |
| 55 | BILL_NOT_PAYED | اگر فاکتوری که پرداخت نشده است را بخواهید ببندید این خطا را دریافت می کنید. |
| 58 | BILL_IS_WAITING_FOR_VERIFICATION | فاکتور تا قبل از تایید شدن قابل بستن نمی باشد. |
| 999 | UNKHOWN | خطای داخلی |
| 4 | PERMISSION_DENIED | اجازه بستن این فاکتور را ندارید |

 <div class="box-end">
</div>

## دریافت لینک پرداخت

ممکن است لازم باشد لینک پرداخت برای مشتری با روش های مختلفی ارسال شود. این لینک قابل اشتراک گذاری خواهد بود و هر کسی که آن را داشته باشد می تواند آن را پرداخت نماید. برای دریافت لینک از تابع زیر استفاده نمایید:

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            GetInvoicePaymentLinkVo getInvoicePaymentLinkVo = new GetInvoicePaymentLinkVo.Builder(baseInfoVo)
                    .setInvoiceId(3581653L)
                    .build();
            billingService.getInvoicePaymentLink(getInvoicePaymentLinkVo, new OnGetResponseListener<String>() {
                @Override
                public void onResponse(ResultVo<String> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


در پاسخ سرویس فوق، لینک ذیل را دریافت خواهید کرد: 

[private-call-address]/v1/pbc/PayInvoiceDispatcher/?h=[hashCode]

که در صورت تمایل، می‌توانید پارامترهای redirectUri ، callbackUri  و "gateway="PEP را نیز ارسال نمایید. اگر پارامتر "gateway="PEP را در لینک بگذارید، کاربر مستقیما به صفحه درگاه پرداخت بانک پاسارگاد هدایت خواهد شد و در صورت ارسال پارامتر redirectUri کاربر ملزم به تکمیل فرآیند خرید، خواهد بود.

توجه داشته باشید که لینک فوق، شامل یک هش کد می‌باشد که مدت اعتبار آن 300 ثانیه می‌باشد؛ لذا در صورتی که با پیغام خطای " کد وارد شده معتبر نمی‌باشد و یا منقضی شده است." روبه‌رو شدید ممکن است کد هش منقضی شده باشد.

 <div class="box-end">
</div>

##  دریافت فایل خروجی فاکتورها

توسط تابع زیر امکان جستجو و دریافت **فایل**فاکتورهای صادر شده توسط کسب و کار قابل انجام خواهد بود و میتوانید ازخروجی این تابع یک **فایل اکسل** با فیلترهای متنوع دریافت کنید.

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken(TOKEN)
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            GetInvoiceListAsFileVo getInvoiceListAsFileVo = new GetInvoiceListAsFileVo.Builder(baseInfoVo)
                    .setLastNRows(10L)
                    .build();
            billingService.getInvoiceListAsFile(getInvoiceListAsFileVo, new OnGetResponseListener<ExportServiceSrv>() {
                @Override
                public void onResponse(ResultVo<ExportServiceSrv> result) {
                    System.out.println(result.getResult().getId());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


بدیهی است در تابع بالا با توجه به اختیاری بودن اکثر فیلدها اگر هیچ یک از پارامترهای اختیاری ارسال نشود گزارش حجیم تر و کاملتری در اکسل خواهید داشت و هرچه تعداد فیلترها بیشتر باشد گزارش دقیق تر و سبک تری در اختیار خواهید داشت.

در صورت موفقیت آمیز بودن سرویس یک شناسه (**ID**) برای فایل ایجاد شده صادر خواهد شد و **statusCode ** برابر با مقدار **EXPORT_SERVICE_STATUS_CREATED **قرار خواهد گرفت در این مرحله باید حدود **1**  تا **2**  دقیقه منتظر بمانید تا **statusCode ** به **EXPORT_SERVICE_STATUS_SUCCESSFUL**  تغییر وضعیت بدهد.

کدهای وضعیتی که ممکن است در حین کار با این تابع مشاهده کنید به شرح زیر میباشد.

EXPORT_SERVICE_STATUS_CREATED // سرویس در حال ایجاد فایل میباشد

EXPORT_SERVICE_STATUS_RUNNING  // فایل در حال آماده سازی میباشد

EXPORT_SERVICE_STATUS_SUCCESSFUL   //  فایل با موفقیت ایجاد شد

EXPORT_SERVICE_STATUS_FAILED // خطایی در ایجاد فایل اتفاق افتاده است

 <div class="box-end">
</div>

## پرداخت فاکتور خارج از پلتفرم پاد

در صورتی که فاکتور به هر شکلی بجز امکانات موجود در پلتفرم پاد پرداخت شد، می‎‌توانید با استفاده از سرویس زیر، وضعیت آن را به حالت پرداخت شده ببرید. در این روش هیچ‌گونه سند مالی در پلتفرم ثبت نشده و به اعتبار افزوده نمی‌شود.

دقت نمایید که کسب و کار فقط می‌تواند فاکتورهایی که خودش صادر نموده را با این روش پرداخت کند.

```
BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            PayInvoiceVo payInvoiceVo = new PayInvoiceVo.Builder(baseInfoVo)
                    .setInvoiceId({invoiceId})
                    .build();
            billingService.payInvoice(payInvoiceVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


 <div class="box-end">
</div>

## پرداخت از کیف پول کسب و کار با توکن کسب و کاری

جهت پرداخت فاکتور با حساب کیف پول کسب و کار در صورتی که فاکتور مشخصا برای شما صادر شده باشد می‌توانید از سرویس زیر استفاده نمایید:

```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setOtt({ott})
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            PayInvoiceByCreditVo payInvoiceByCreditVo = new PayInvoiceByCreditVo.Builder(baseInfoVo)
                    .setInvoiceId({invoiceId})
                    .build();
            billingService.payInvoiceByCredit(payInvoiceByCreditVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


در صورتی که فاکتور برای شما صادر نشده یا اصلا کاربر ندارد، جهت پرداخت آن از سرویس زیر استفاده نمایید:

```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setOtt({ott})
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            PayAnyInvoiceByCreditVo payAnyInvoiceByCreditVo = new PayAnyInvoiceByCreditVo.Builder(baseInfoVo)
                    .setInvoiceId({invoiceId})
                    .setWallet("{walletCode}")
                    .build();
            billingService.payAnyInvoiceByCredit(payAnyInvoiceByCreditVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


 <div class="box-end">
</div>

## پرداخت از طریق درگاه

کسب و کار می‌تواند برای تمام مشتریان خود، بدون نیاز به ورود به سامانه احراز هویت یکپارچه، امکان خرید را از طریق لینک زیر فراهم کند. برای این منظور لازم است کسب و کار از کد یکتا که برای فاکتور تولید می‌شود استفاده نماید.

مراحل انجام کار به ترتیب:

1. [ثبت نام کسب و کار](https://docs.pod.land/document/Business-Requirements-BusinessRegister) در [https://services.pod.land](https://panel.pod.land/Home/AddBusiness)
2. [دریافت توکن جهت فراخوانی سرویس ها](http://docs.pod.land/document/Business-Keys-Add)
3. [ثبت فاکتور](https://docs.pod.land/document/Developer-Invoice-IssueInvoiceByBiz): دقت نمایید در صورت تمایل به نمایش شماره کارت های مربوط به مشتری، در صفحه درگاه ضروری است شناسه کاربر (userId) در فاکتور ثبت شود. این شناسه پس از ورود کاربر از طریق SSO بدست آمده یا می تواند شناسه ی کاربر آفلاین (غیر SSO) باشد. در صورتی که شماره موبایل مربوط به هیچکدام از این دودسته نیست، می توان با ثبت شماره موبایل (cellphoneNumber) در فاکتور، همین نتیجه را دریافت نمود.
4. 			هدایت کاربر به درگاه (توسط لینک زیر)
5. [تایید پرداخت](https://docs.pod.land/document/Developer-Invoice-VerifyInvoice)
6. [بستن فاکتور](https://docs.pod.land/document/Developer-Invoice-CloseInvoice)
7. [تسویه](https://docs.pod.land/document/Developer-WalletOperation-SettlementRequest)

```
   BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        try {
            PayInvoiceByUniqueNumberVo payInvoiceByUniqueNumberVo = new PayInvoiceByUniqueNumberVo.Builder(baseInfoVo)
                    .setUniqueNumber({uniqueNumber})
                    .setGateway("PEP")
                    .setRedirectUri("{redirectUri}")
                    .build();
            return payInvoiceByUniqueNumberVo.getLink();

        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
        return null;

    }
```


 <div class="box-end">
</div>

## پرداخت فاکتور با کیف پول از طریق پیامک

در صورتی که کاربر به رایانه جهت پرداخت دسترسی ندارد، یا در فروش حضوری، کسب و کار میتواند درخواست ارسال پیامک پرداخت به کاربر دهد و کاربر با پیامک کردن کدی که دریافت کرده به همان شماره، فاکتور را از کیف پول خود پرداخت مینماید.

```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            SendInvoicePaymentSmsVo sendInvoicePaymentSMSVo = new SendInvoicePaymentSmsVo.Builder(baseInfoVo)
                    .setInvoiceId({invoiceId})
                    .build();
            billingService.sendInvoicePaymentSMS(sendInvoicePaymentSMSVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


 <div class="box-end">
</div>

## پرداخت فاکتور از طریق فاکتور

از طریق این سرویس کسب و کار قادر خواهد بود که پرداخت شدن برخی فاکتورهای خود را منوط به پرداخت شدن فاکتورهای دیگری نماید. یا به عبارتی نوعی تهاتر را بوسیله فاکتورها انجام دهد که این امر توسط سرویس زیر قابل اجرا خواهد بود

```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            PayInvoiceByInvoiceVo payInvoiceByInvoiceVo = new PayInvoiceByInvoiceVo.Builder(baseInfoVo)
                  .setCreditorInvoiceId({creditorInvoiceId})
                    .setDebtorInvoiceId({debtorInvoiceId})
                    .build();
            billingService.payInvoiceByInvoice(payInvoiceByInvoiceVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```


 <div class="box-end">
</div>

## پرداخت فاکتور در آینده

از طریق این سرویس کسب و کار قادر خواهد بود فاکتورهایی که برایش توسط دیگران صادر شده را درتاریخ آینده یا سررسید توافقی از طریق مبلغی که در کیف پول یا اصناف خود دارد  پرداخت نماید .

این سرویس باید توسط کسب و کار یا کاربر بدهکار یا شخصی که فاکتور برایش صادر شده صدا زده شود در غیر این صورت با خطای زیر روبرو خواهد شد

```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setOtt({ott})
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        BillingService billingService = new BillingService();

        try {
            PayInvoiceInFutureVo payInvoiceInFutureVo = new PayInvoiceInFutureVo.Builder(baseInfoVo)
                    .setDate()
                    .setInvoiceId({invoiceId})
                    .setGuildCode({guildCode})
                    .build();
            billingService.payInvoiceInFuture(payInvoiceInFutureVo, new OnGetResponseListener<Boolean>() {
                @Override
                public void onResponse(ResultVo<Boolean> result) {
                    System.out.println(result.getResult());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }
```

 <div class="box-end">
</div>
