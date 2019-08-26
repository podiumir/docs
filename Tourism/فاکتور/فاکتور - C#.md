# فاکتور
## صدور فاکتور توسط کسب وکار 
هرگونه پرداخت در پلتفرم پاد، از طریق فاکتور صورت می‌گیرد. در این بخش صدور فاکتور با استفاده از توکن کسب‌و‌کار شرح داده شده و می‌توان با خروجی حاصل از این متد، کاربر را به راحتی به درگاه پرداخت هدایت نمود. برای  صدور فاکتور از سرویس زیر استفاده نمایید. شبه کد زیر یک فاکتور با دو بند  فاکتور را شامل می شود:
پارامترهای اختیاری کامنت شده اند,برای استفاده می توانید از حالت کامنت خارج کنید.

```
var output = new ResultSrv<InvoiceSrv>();
                var invoiceSrv = IssueInvoiceVo.ConcreteBuilder
                    .SetGuildCode("{put your guildCode}")
                    .SetProductsInfo(new List<ProductInfo>
                    {                         
               ProductInfo.ConcreteBuilder.SetProductId(0).SetPrice(1000).SetQuantity(3).SetProductDescription("tst1").Build(),                         
                ProductInfo.ConcreteBuilder.SetProductId(0).SetPrice(1000).SetQuantity(3).SetProductDescription("tst1").Build()
                    })
                    .SetOtt("{Put your ott}")
                    //.SetPreview({put your preview})
                    //.SetMetadata("{put your metadata}")
                    //.SetUserId({put user id})
                    //.SetAddressId("{put your addressId}")
                    .Build(); // Create new instance 
 billingService.IssueInvoice(invoiceSrv, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## لیست آدرس
در صورتی که تمایل به ارسال آدرس مشتری دارید، از طریق سرویس زیر شناسه‌های آدرس‌های موجود برای کاربر را استخراج نمایید.
 پارامترهای اختیاری کامنت شده اند,برای استفاده می توانید از حالت کامنت خارج کنید.

```
 var output = new ResultSrv<AddressSrv>();
                var invoiceSrv = ListAddressVo.ConcreteBuilder
                    .SetOffset("0")
                    //.SetSize("")
                    .Build();
 billingService.GetListAddress(invoiceSrv, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## تایید پرداخت فاکتور

در صورتی که در صدور فاکتور پارامتر verificationNeeded را با مقدار true  ارسال نموده باشید، پرداخت سه مرحله ای فعال شده است. به این معنی که پس از هدایت کاربر به صفحه پرداخت(فقط در صورت پرداخت فاکتور از طریق اتصال به  درگاه می توانید سرویس تایید فاکتور را صدا بزنید) و دریافت پاسخ در redirectUri لازم است پرداخت توسط کسب و کار با استفاده از API زیر تایید شود. 
در صورتی که فاکتور مورد نظر تسهیمی است، شناسه ای که باید به این سرویس  ارسال گردد، معادل result -> id موجود در خروجی فاکتور تسهیمی می باشد.
پارامترهای اختیاری کامنت شده اند,برای استفاده می توانید از حالت کامنت خارج کنید.

```
var output = new ResultSrv<InvoiceSrv>();
var verifyInvoiceVo = VerifyInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    //.SetBillNumber("{put your billNumber}")
                    .Build();
billingService.VerifyInvoice(verifyInvoiceVo, response => Listener.GetResult(response, out output));
```



<div class="box-end">
</div>

## بستن فاکتور
فاکتور هایی که بسته شوند دیگر قابل ابطال نیستند. برای اینکه بتوانید مبالغ فروش خود را تسویه نمایید لازم است حتما فاکتورها را ببندید.

```
var output = new ResultSrv<bool>();
var closeInvoiceVo = CloseInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    .Build();
billingService.CloseInvoice(closeInvoiceVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## تایید و بستن در یک مرحله
با فراخوانی سرویس زیر، می‌توانید همزمان تایید و بستن فاکتور را انجام دهید.

```
var output = new ResultSrv<InvoiceSrv>();
var verifyAndCloseInvoiceVo = VerifyAndCloseInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    .Build();
billingService.VerifyAndCloseInvoice(verifyAndCloseInvoiceVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## ابطال فاکتور
در صورتی که فاکتور باطل شود، دیگر قابل پرداخت نیست و در صورتی که قبلا پرداخت شده باشد، مبلغ آن به پرداخت کننده برگشت خواهد خورد. 
توجه: در صورتی که فاکتور با شرایط safe=true صادر شده باشد، فقط پرداخت  کننده می تواند فاکتور را کنسل کند و اگر safe نباشد فقط issuer فاکتور  مجاز به کنسلی فاکتور می باشد. 
```
var output = new ResultSrv<bool>();
var cancelInvoiceVo = CancelInvoiceVo.ConcreteBuilder
                    .SetId({put your id})
                    .Build();
billingService.CancelInvoice(cancelInvoiceVo, response => Listener.GetResult(response, out output));
```



<div class="box-end">
</div>

## دریافت فاکتور
با فراخوانی سرویس زیر می توانید فاکتورهایی که کسب و کار شما صادر نموده و همچنین وضعیت آنها را مشاهده نمایید.

```
var output = new ResultSrv<List<InvoiceSrv>>();
var getInvoiceListVo = GetInvoiceListVo.ConcreteBuilder
                    .SetSize({Put your size})
                    .SetOffset({Put your offset})
                    //.SetGuildCode("{put your guildCode}")
                    .Build();
billingService.GetInvoiceList(getInvoiceListVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## دریافت فاکتور با متا دیتا
از طریق این سرویس می توانید تمام فاکتورهایی که برای آنها متادیتا تعریف کرده اید دریافت کنید. 
در قسمت metaQuery مقادیر درخواستی خود را به فرم json با استفاده از توصیحات جستجوی متادیتا ارسال نمایید.
https://docs.pod.land/v1.0.8.0/Developer/CustomPost/400/SearchMetadata

```
var output = new ResultSrv<List<InvoiceSrv>>();
var getInvoiceListByMetadataVo = GetInvoiceListByMetadataVo.ConcreteBuilder
                    //.SetMetaQuery("{Put your metaQuery}")
                    //.SetSize({Put your size})
                    //.SetOffset({Put your offset})
                    //.SetIsCanceled({put your value})
                    //.SetIsPayed({put your value})
                    .Build();
billingService.GetInvoiceListByMetadata(getInvoiceListByMetadataVo, response => Listener.GetResult(response, out output));
```



<div class="box-end">
</div>

## دریافت لیست فاکتورها در قالب فایل
از طریق سرویس زیر امکان دریافت لیست فاکتورها در قالب فایل وجود دارد. 
وارد کردن یکی از فیلدهای زیر ضروری است : lastNRows,fromDate,toDate

```
var output = new ResultSrv<InvoiceSrv>();
var getInvoiceListAsFileVo = GetInvoiceListAsFileVo.ConcreteBuilder
                    .SetLastNRows({Put your LastNRows})
                    //.SetFromDate({Put your FromDate})
                    //.SetToDate({Put your ToDate})
                    //.SetGuildCode("{Put your GuildCode}")
                    //.SetId({Put your Id})
                    //.SetBillNumber("{Put your BillNumber}")
                    //.SetUniqueNumber("{Put your UniqueNumber}")
                    //.SetTrackerId({Put your TrackerId})
                    //.SetIsCanceled({Put your IsCanceled})
                    //.SetIsClosed({Put your IsClosed})
                    //.SetIsPayed({Put your IsPayed})
                    //.SetIsWaiting({Put your IsWaiting})
                    //.SetReferenceNumber("{Put your ReferenceNumber}")
                    //.SetUserId({Put your UserId})
                    //.SetQuery("{Put your Query}")
                    //.SetProductIdList({Put your ProductIdList})
                    //.SetCallbackUrl("{Put your CallbackUrl}")
                    .Build();
billingService.GetInvoiceListAsFile(getInvoiceListAsFileVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## کاهش فاکتور
در مواردی ممکن است نیاز به تغییری در بندهای فاکتور داشته باشید. در صورتی که فاکتور پرداخت نشده است، فاکتور قبلی را باطل (cancel) نمایید و فاکتور جدیدی صادر کنید. اگر فاکتور پرداخت شده است(در صورتی که باید پول بیشتری از مشتری دریافت نمایید)، لازم است فاکتوری جداگانه به مبلغ افزوده شده، با ذکر دلیل صادر نموده و مشتری را مجددا برای پرداخت هدایت نمایید. در برخی مواقع لازم است مبلغی از فاکتور پرداخت شده به مشتری بازگردانده شود. برای این منظور از API زیر برای اصلاح فاکتور پرداخت شده استفاده نمایید.

```
var output = new ResultSrv<InvoiceSrv>();
var reduceInvoiceVo = ReduceInvoiceVo.ConcreteBuilder
                    .SetId({Put your id})
                    .SetInvoiceItemsInfo(new List<InvoiceItemInfoVo>
                    {
                        InvoiceItemInfoVo.ConcreteBuilder.SetInvoiceItemId({Put your id}).SetItemDescription("{Put your description}").SetPrice({Put your price}).SetQuantity({Put your quantity}).Build(),
                        InvoiceItemInfoVo.ConcreteBuilder.SetInvoiceItemId({Put your id}).SetItemDescription("{put your description}").SetPrice({Put your price}).SetQuantity({Put your quantity}).Build()
                    })
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    .Build();
billingService.ReduceInvoice(reduceInvoiceVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## دریافت لینک دانلود فایل های اکسل
جهت مشاهده وضعیت هریک از سرویس های درخواست داده شده خود برای دریافت فایل خروجی فاکتورها  میتوانید از سرویس
زیر استفاده نمایید.
در صورتی که وضعیت سرویس موفقیت آمیز بوده باشد از طریق تابع GetLink  میتوانید به لینک فایل ایجاد شده توسط سیستم دسترسی داشته باشید.مقادیر hashCode و fileId را پس از دریافت از سرویس GetExportList در تابع GetLink جایگذاری نمایید.

```
var output = new ResultSrv<List<ExportServiceSrv>>();
var getExportListVo = GetExportListVo.ConcreteBuilder
                    .SetOffset({Put your Offset})
                    //.SetSize({Put your Size})
                    //.SetId({Put your Id})
                    //.SetStatusCode({Put your StatusCode})
                    //.SetServiceUrl("{Put your ServiceUrl}")
                    .Build();
billingService.GetExportList(getExportListVo, response => Listener.GetResult(response, out output));
var link=getExportListVo.GetLink({Put your FileId}, "{Put your HashCode}");
```



<div class="box-end">
</div>

## پرداخت فاکتور خارج از پلتفرم پاد
در صورتی که فاکتور به هر شکلی بجز امکانات موجود در پلتفرم پادپرداخت شد، میتوانید با استفاده از سرویس زیر، وضعیت آن را به حالت پرداخت شده ببرید. در این روش هیچ گونه سند مالی در پلتفرم ثبت نشده و به اعتبار افزوده نمی شود. دقت نمایید که کسب و کار فقط می تواند فاکتورهایی که خودش صادر نموده را با این روش پرداخت کند.

```
var output = new ResultSrv<bool>();
var payInvoiceVo = PayInvoiceVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    .Build();
billingService.PayInvoice(payInvoiceVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## پرداخت فاکتور با کیف پول از طریق پیامک
در صورتی که کاربر به رایانه جهت پرداخت دسترسی ندارد، یا در فروش حضوری، کسب و کار میتواند درخواست ارسال پیامک
پرداخت به کاربر دهد و کاربر با پیامک کردن کدی که دریافت کرده به همان شماره، فاکتور را از کیف پول خود پرداخت مینماید.

```
var output = new ResultSrv<bool>();
var sendInvoicePaymentSmsVo = SendInvoicePaymentSmsVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    //.SetWallet("{Put your Wallet}")
                    //.SetCallbackUri("Put your CallbackUri")
                    //.SetRedirectUri("Put your RedirectUri")
                    //.SetDelegationId({Put your DelegationId})
                    //.SetForceDelegation({Put your ForceDelegation})
                    .Build();
billingService.SendInvoicePaymentSms(sendInvoicePaymentSmsVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## پرداخت فاکتور در آینده
از طریق این سرویس کسب و کار قادر خواهد بود فاکتورهایی که برایش توسط دیگران صادر شده را درتاریخ آینده یا سررسید توافقی از طریق مبلغی که در کیف پول یا اصناف خود دارد  پرداخت نماید.
این سرویس باید توسط کسب و کار یا کاربر بدهکار یا شخصی که فاکتور برایش صادر شده صدا زده شود در غیر این صورت با خطای "فاکتور برای شما صادر نشده است" روبرو خواهد شد.

```
var output = new ResultSrv<bool>();
var ottOutput = GetOtt();
var payInvoiceInFutureVo = PayInvoiceInFutureVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    .SetDate("{Put your Date}")
                    .SetOtt(ottOutput.Ott)
                    //.SetGuildCode("{Put your GuildCode}")
                    //.SetWallet("{Put your Wallet}")
                    .Build();
billingService.PayInvoiceInFuture(payInvoiceInFutureVo,response => Listener.GetResult(response, out output));
```



<div class="box-end">
</div>

## پرداخت فاکتور از طریق فاکتور
از طریق این سرویس کسب و کار قادر خواهد بود که پرداخت شدن برخی فاکتورهای خود را منوط به پرداخت شدن فاکتورهای دیگری
نماید. یا به عبارتی نوعی تهاتر را بوسیله فاکتورها انجام دهد که این امر توسط سرویس زیر قابل اجرا خواهد بود.

```
var output = new ResultSrv<bool>();
var payInvoiceByInvoiceVo = PayInvoiceByInvoiceVo.ConcreteBuilder
                    .SetCreditorInvoiceId({Put your CreditorInvoiceId})
                    .SetDebtorInvoiceId({Put your DebtorInvoiceId})
                    .Build();
billingService.PayInvoiceByInvoice(payInvoiceByInvoiceVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## نمایش پیش فاکتور
در پلتفرم کسب و کار، فاکتورهایی که پرداخت می شوند به صورت سالانه شماره سریال دریافت می نمایند، بنابرین کسب و کار می
تواند برای امور مالی خود به آن شماره سریال استناد نماید. در برخی شرایط، ممکن است کسب و کار بخواهد فاکتور تا زمانی که اقدام به پرداخت آن نشده اصلاً ثبت نگردد. بدین منظور با استفاده از سرویس زیر می تواند پیش فاکتور را ثبت نماید و با لینک بعدی آن را نمایش دهد. به محض اینکه مشتری، فاکتور را با کیف پول خود پرداخت نماید یا برای پرداخت وارد درگاه بانکی شود، فاکتور ثبت می گردد. در صورتی که مشتری پرداخت را از طریق درگاه لغو نماید یا اشکالی در پرداخت او به وجود آید، فاکتور به صورت خودکار لغو خواهد شد. 
دریافت می نمایید .
در پاسخ درخواست سرویس CreatePreInvoice یک کد hash دریافت می نمایید که  باید از طریق  ()createPreInvoiceVo.GetLink لینک را دریافت کرده و کاربر  را به آن آدرس هدایت کنید.

```
var output = new ResultSrv<string>();
var ottOutput = GetOtt();
var createPreInvoiceVo = CreatePreInvoiceVo.ConcreteBuilder
                    .SetToken({Put your ApiToken})
                    .SetOtt(ottOutput.Ott)
                    .SetProductsInfo(new List<ProductInfo>
                    {
                        ProductInfo.ConcreteBuilder.SetProductId({Put your ProductId}).SetPrice({Put your Price}).SetQuantity({Put your Quantity}).SetProductDescription("{Put your ProductDescription}").Build(),
                        ProductInfo.ConcreteBuilder.SetProductId({Put your ProductId}).SetPrice({Put your Price}).SetQuantity({Put your Quantity}).SetProductDescription("{Put your ProductDescription}").Build()
                    })
                    .SetGuildCode("{Put your GuildCode}")
                    .SetRedirectUri("{Put your RedirectUri}")
                    .SetUserId({Put your UserId})
                    //.SetBillNumber("{Put your BillNumber}")
                    //.SetCallUrl("{Put your CallUrl}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetDeadline("{Put your Deadline}")
                    //.SetDescription("{Put your Description}")
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    //.SetRedirectUri("{Put your RedirectUri}")
                    //.SetVerificationNeeded({Put your VerificationNeeded})
                    .Build();
billingService.CreatePreInvoice(createPreInvoiceVo,response => Listener.GetResult(response, out output));
var linkSrv = createPreInvoiceVo.GetLink(output.Result);

```



<div class="box-end">
</div>

## پرداخت از کیف پول با ورود به SSO
مشتری برای مشاهده فاکتور خود و پرداخت آن از طریق کیف پول خود، لازم است از طریق آدرسی که تابع ()payInvoiceByWalletVo.GetLink  بعنوان خروجی می دهد هدایت شود.
مقدار invoiceId، مقداری است که از پاسخ سرویس issueInvoice با عنوان id  دریافت می‌نمایید و این مقدار از billNumber که توسط خود کسب و کار انتخاب  شده است، متمایز می‌باشد.
در این حالت، مشتری باید لاگین باشد و در صورتی که شناسه اشتباه وارد شود با خطای " فاکتور یافت نشد " مواجه می شود.
```
 var payInvoiceByWalletVo = PayInvoiceByWalletVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    //.SetCallUri("{Put your CallUri}")
                    //.SetRedirectUri("{Put your RedirectUri}")
                    .Build();
var output = payInvoiceByWalletVo.GetLink();

```



<div class="box-end">
</div>

## دریافت لینک پرداخت 
ممکن است لازم باشد لینک پرداخت برای مشتری با روش های مختلفی ارسال شود. این لینک قابل اشتراک گذاری خواهد بود و هر کسی که آن را داشته باشد می تواند آن را پرداخت نماید. برای دریافت لینک از سرویسGetInvoicePaymentLink استفاده نمایید.
در پاسخ سرویس فوق یک لینک دریافت خواهید کرد که در صورت تمایل، می‌توانید  پارامترهای redirectUri ، callbackUri و "gateway="PEP را به تایع ()getInvoicePaymentLinkVo.GetAdvanceLink ارسال نمایید و لینک خود را دریافت نمایید. اگر پارامتر "gateway="PEP را  بگذارید، لینک تولید شده کاربر را مستقیما به صفحه درگاه پرداخت بانک  پاسارگاد هدایت خواهد شد و در صورت ارسال پارامتر redirectUri کاربر ملزم  به تکمیل فرآیند خرید، خواهد بود. 
توجه داشته باشید که لینک فوق، شامل یک هش کد می‌باشد که مدت اعتبار آن 300 ثانیه می‌باشد؛لذا در صورتی که با پیغام خطای " کد وارد شده معتبر نمی‌باشد و یا منقضی شده است." روبه‌رو شدید ممکن است کد هش منقضی شده باشد.

```
var output = new ResultSrv<string>();
var getInvoicePaymentLinkVo = GetInvoicePaymentLinkVo.ConcreteBuilder
                    .SetInvoiceId({Put your InvoiceId})
                    .Build();
billingService.GetInvoicePaymentLink(getInvoicePaymentLinkVo,response => Listener.GetResult(response, out output));
var advanceLink = getInvoicePaymentLinkVo.GetAdvanceLink(output.Result, "PEP");

```



<div class="box-end">
</div>

## پرداخت پیشرفته 
کسب و کار میتواند برای تمام مشتریان خود، بدون نیاز به ورود به سامانه احراز هویت یکپارچه، امکان خرید را از طریق لینک ()payInvoiceByUniqueNumberVo.GetLink  فراهم کند. برای این منظور لازم است کسب و کار از کد یکتا که برای فاکتور تولید می شود استفاده نماید. مراحل انجام کار به ترتیب:

1. ثبت نام کسب و کار در
https://services.pod.land

2. دریافت توکن جهت فراخوانی سرویس ها

3. ثبت فاکتور : دقت نمایید در صورت تمایل به نمایش شماره کارت های مربوط به  مشتری، در صفحه درگاه ضروری است شناسه کاربر (userId) در فاکتور ثبت شود.  این شناسه پس از ورود کاربر از طریق SSO بدست آمده یا می تواند شناسه ی  کاربر آفلاین (غیر SSO) باشد. در صورتی که شماره موبایل مربوط به هیچکدام  از این دودسته نیست، می توان با ثبت شماره موبایل (cellphoneNumber) در فاکتور، همین نتیجه را دریافت نمود.

4.  هدایت کاربر به درگاه ( از طریق  ()payInvoiceByUniqueNumberVo.GetLink لینک را دریافت نمایید )

5. تایید پرداخت

6.بستن فاکتور

7. تسویه

پارامتر redirectUri آدرسی است که بعد از پرداخت کاربر به آن هدایت می  گردد، پارامتر callUri نیز آدرسی در سرور شما میتواند باشد که در صورت موفق بودن پرداخت فراخوانی می گردد. پس از پرداخت پارمترهای زیر به صورت GET به  آدرس redirectUri برگردانده می شود. توجه: در صورتی که پارامتر gateway ارسال شود کاربر مستقیم به درگاه پرداخت بانک پاسارگاد متنقل می گردد. اگر مقدار uniqueNumber اشتباه ارسال شود، به صفحه "صفحه یافت نشد" هدایت می شوید.

```
var payInvoiceByUniqueNumberVo = PayInvoiceByUniqueNumberVo.ConcreteBuilder
                    .SetUniqueNumber("{Put your UniqueNumber}")
                    //.SetGateway("{Put your Gateway}")
                    //.SetRedirectUri("{Put your RedirectUri}")
                    //.SetCallUri("{Put your CallUri}")
                    .Build();
var output = payInvoiceByUniqueNumberVo.GetLink();

```



<div class="box-end">
</div>

## تسویه از حساب مشتری (برداشت از کیف پول)
کسب و کار می تواند از طریق سرویس RequestSettlement  و ایجاد نمونه از کلاس RequestWalletSettlementVo ،
مبلغ مورد نظر خود را از کیف پولش به شماره شبای ثبت شده در پروفایل خود منتقل کند. در صورتی که شماره شبا یا نام و نام خانوادگی شخص در پروفایل ثبت نشده باشد این سرویس خطا خواهد داد. کد ارز شامل کد سه حرفی رایج برای واحدهای پولی است. مانند
IRR و USD

```
var ottOutput = GetOtt();
var output = new ResultSrv<SettlementRequestSrv>();
var requestWalletSettlementVo= RequestWalletSettlementVo.ConcreteBuilder
                    .SetAmount({Put your Amount})
                    .SetOtt(ottOutput.Ott)
                    //.SetWallet("{Put your Wallet}")
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetDescription("{Put your Description}")
                    .Build();
billingService.RequestSettlement(requestWalletSettlementVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## تسویه از حساب صنفی کسب و کار
در حساب های صنفی همواره مبلغی به عنوان مبلغ قابل تسویه وجود دارد که شامل دارایی کسب و کار بجز فاکتورهای باز او یا فاکتورهایی که مبلغ آن ها هنوز واریز نشده است، می باشد. مبلغ قابل تسویه را می توان از طریق RequestSettlement و ایجاد نمونه از کلاس RequestGuildSettlementVo تسویه نمود. کد ارز شامل کد سه حرفی رایج برای واحدهای پولی است. مانند
IRR و USD

```
var ottOutput = GetOtt();
var output = new ResultSrv<SettlementRequestSrv>();
var requestGuildSettlementVo= RequestGuildSettlementVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    .SetAmount({Put your Amount})
                    .SetOtt(ottOutput.Ott)
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetDescription("{Put your Description}")
                    .Build();
billingService.RequestSettlement(requestGuildSettlementVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

##انتقال وجه از حساب کسب و کاری به کارت بانکی (با کسر کارمزد) یا شماره شبا
کسب و کار می تواند با استفاده از سرویس زیر مبلغ مورد نظر خود را از حساب مجازی به یک شماره کارت یا یک شماره شبا بانکی منتقل نماید. بدیهی است که در صورت استفاده از ابزار کارت به کار، کارمزد بانکی از حساب کسب و کار کسر خواهد شد و در صورت استفاده از ابزار پایا، انتقال وجه در زمان مصوب بانک مرکزی انجام خواهد شد. برای پارامتر toolCode از یکی از مقادیر زیر استفاده نمایید:
SETTLEMENT_TOOL_SATNA
SETTLEMENT_TOOL_PAYA
SETTLEMENT_TOOL_CARD
   و به طور مثال، در صورتی که انتقال از طریق کارت را انتخاب نموده اید، در قسمت toolId شماره کارت مقصد را وارد نمایید و در غیر این صورت شماره شبا را وارد نمایید. کد ارز شامل کد سه حرفی رایج برای واحدهای پولی است. مانند IRR و USD

```
var ottOutput = GetOtt();
var output = new ResultSrv<SettlementRequestSrv>();
var requestSettlementByToolVo = RequestSettlementByToolVo.ConcreteBuilder
                    .SetToolCode({Put your ToolCode})
                    .SetToolId("{Put your ToolId}")
                    .SetAmount("{Put your Amount}")
                    .SetGuildCode("{Put your GuildCode}")
                    .SetOtt(ottOutput.Ott)
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetDescription("{Put your Description}")
                    .Build();
billingService.RequestSettlement(requestSettlementByToolVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## گزارش وضعیت تسویه
جهت دریافت لیست تسویه ها و وضعیت آن ها از سرویس ListSettlements استفاده نمایید.
```
var output = new ResultSrv<List<SettlementRequestSrv>>();
var listSettlementsVo = ListSettlementsVo.ConcreteBuilder
                    .SetOffset({Put your Offset})                    
                    //.SetSize({Put your Size})
                    //.SetStatusCode({Put your StatusCode})
                    //.SetFromAmount({Put your FromAmount})
                    //.SetToAmount({Put your ToAmount})
                    //.SetFromDate("{Put your FromDate}")
                    //.SetToDate({Put your ToDate})
                    //.SetUniqueId("{Put your UniqueId}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    .Build();
billingService.ListSettlements(listSettlementsVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## فعالسازی تسویه خودکار در صورتی
که تسویه خودکار برای یک کسب و کارفعال شود، مبلغ قابل تسویه آن کسب و کار به طور خودکار، یکبار در شبانه روز به شماره شبای اعلام شده در پروفایل کسب و کار یا شماره شبای اعلامی در سرویس زیر، تسویه می گردد. برای فعالسازی تسویه خودکار سرویس زیر را با توکن کسب و کار دارنده حساب فراخوانی نمایید.

```
var ottOutput = GetOtt();
var output = new ResultSrv<bool>();
var addAutoSettlementVo = AddAutoSettlementVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    .SetOtt(ottOutput.Ott)
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    //.SetInstant({Put your Instant})
                    .Build();
billingService.AddAutoSettlement(addAutoSettlementVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## لغو تسویه خودکار
با سرویس زیر می‌توانید تسویه خودکار را غیرفعال نمایید.

```
var output = new ResultSrv<bool>();
var registerUserVo = RemoveAutoSettlementVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    //.SetCurrencyCode("{Put your CurrencyCode}")
                    .Build();
billingService.RemoveAutoSettlement(registerUserVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## اجازه ثبت فاکتور
در صورتی که بخشی از فروش شما به کسب و کار دیگری تعلق دارد و میخواهید فاکتور به نام همان کسب و کار ثبت شود، لازم است آن کسب و کار به کسب و کار شما اجازه صدور فاکتور به عنوان معامله گر را داده باشد. برای این منظور خود کسب و کار ذینفع یا کارگزار او، با استفاده از توکن که در اختیار دارد، با استفاده از سرویس زیر به کسب کار دیگر اجازه صدور فاکتور می دهد.

```
var output = new ResultSrv<BusinessDealerSrv>();
var addDealerVo = AddDealerVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    //.SetAllProductAllow({Put your AllProductAllow})
                    .Build();
billingService.AddDealer(addDealerVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## دریافت لیست کسب و کارها
برای دریافت یا جستجوی لیست تمام کسب و کارهایی که به آنها مجوز معامله و صدور فاکتور داده اید، از سرویس زیر استفاده نمایید.
توجه داشته باشید در صورتی که شناسه کسب و کار را اشتباه وارد کنید، با اررور "شناسه کسب و کار یافت نشد" مواجه نخواهید شد بلکه در فایل خروجی هیچ مقداری دریافت نخواهید کرد.
(با hasError": false")
```
var output = new ResultSrv<List<BusinessDealerSrv>>();
var dealerListVo = DealerListVo.ConcreteBuilder
                    //.SetDealerBizId(0)
                    //.SetEnable(false)
                    //.SetOffset(0)
                    //.SetSize(0)
                    .Build();
billingService.DealerList(dealerListVo, response => Listener.GetResult(response, out output));
```



<div class="box-end">
</div>

## فعالسازی مجوز معامله گران
برای فعالسازی مجوز معامله گران، به ترتیب از سرویس  زیر استفاده نمایید.

```
var output = new ResultSrv<BusinessDealerSrv>();
 var enableDealerVo = EnableDealerVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.EnableDealer(enableDealerVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## فعالسازی مجوز معامله گران
برای غیر فعالسازی مجوز معامله گران، از سرویس  زیر استفاده نمایید.

```
var output = new ResultSrv<BusinessDealerSrv>();
 var enableDealerVo = EnableDealerVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.EnableDealer(enableDealerVo, response => Listener.GetResult(response, out output));
```



<div class="box-end">
</div>

## لیست کسب و کارهایی که واسط آن هستید
با فراخوانی سرویس زیر می توانید لیست کسب و کارهایی که واسط آن ها شده اید را دریافت نمایید.

```
var output = new ResultSrv<List<BusinessDealerSrv>>();
var businessDealingListVo = BusinessDealingListVo.ConcreteBuilder
                    .SetDealerBizId({Put your DealerBizId})
                    //.SetEnable({Put your Enable})
                    //.SetOffset({Put your Offset})
                    //.SetSize({Put your Size})
                    .Build();
billingService.BusinessDealingList(businessDealingListVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## صدور فاکتور تسهیمی

این نوع فاکتور برای زمانی مناسب است که شما بخواهید محصولات یا خدمات سایر کسب و کارها را به فروش برسانید و یا در بازی‌ها بخواهید برای طراح، برنامه‌نویس، تولید‌کننده‌ی محتوا و ... سهم‌های جداگانه در نظر بگیرید. در این شرایط می‌توانید نوعی فاکتور با قوانین تسهیم فروش صادر نمایید. ظاهراً خریدار تغییری را احساس نخواهد کرد و یک فاکتور تجمیعی را پرداخت می‌­کند. ولی در عمل، به تعداد ذینفعان با مبلغ تسهیمی، فاکتور صادر شده و مبا‌لغ مستقیماً پس از پرداخت به حساب آن‌­ها منتقل می‌شود.

کسب و کار معامله گر که لازم است فاکتور تسهیمی صادر نماید باید از جانب کسب و کارهای سهیم دارای مجوز صدور فاکتور باشد. سپس می‌تواند با استفاده از سرویس زیر تسهیم فروش انجام دهد.

```
var output = new ResultSrv<InvoiceSrv>();
var ottOutput = GetOtt();
var mainInvoiceVos = MainInvoiceVo.ConcreteBuilder
                    .SetGuildCode("{Put your GuildCode}")
                    .SetInvoiceItemVOs(new List<InvoiceItemVo>
                    {
                        InvoiceItemVo.ConcreteBuilder.SetProductId({Put your ProductId}).SetDescription("{Put your 
                        Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                    })
                    //.SetBillNumber("{Put your BillNumber}")
                    //.SetDescription("{Put your Description}")
                    //.SetMetadata("{Put your Metadata}")
                    .Build();

var subInvoiceVos = new List<SubInvoiceVo>
                {
                    SubInvoiceVo.ConcreteBuilder
                        .SetBusinessId({Put your BusinessId})
                        .SetGuildCode("{Put your GuildCode}")
                        .SetInvoiceItemVOs(new List<InvoiceItemVo>
                        {
                            InvoiceItemVo.ConcreteBuilder.SetProductId({Put your ProductId}).SetDescription("{Put your 
                            Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                        })
                        //.SetBillNumber("{Put your BillNumber}")
                        .SetDescription("{Put your Description}")
                        //.SetMetadata("{Put your Metadata}")
                        .Build()

                };
var customerInvoiceItems = new List<InvoiceItemVo>
                {
                    InvoiceItemVo.ConcreteBuilder.SetProductId({Put your ProductId}).SetDescription("{Put your 
                            Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                };
                var multiInvoiceData = MultiInvoiceDataVo.ConcreteBuilder
                    .SetMainInvoice(mainInvoiceVos)
                    .SetSubInvoices(subInvoiceVos)
                    .SetCustomerInvoiceItemVOs(customerInvoiceItems)
                    //.SetPreview({Put your Preview})
                    //.SetCurrencyCode("Put your CurrencyCode")
                    //.SetCustomerDescription("{Put your CustomerDescription}")
                    //.SetCustomerMetadata("{Put your CustomerMetadata}")
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    //.SetRedirectUrl("{Put your RedirectUrl}")
                    //.SetUserId({Put your UserId})
                    //.SetVerificationNeeded({Put your VerificationNeeded})
                    //.SetVoucherHashs({Put your VoucherHashs})
                    .Build();

var issueMultiInvoiceVo = IssueMultiInvoiceVo.ConcreteBuilder
                    .SetOtt(ottOutput.Ott)
                    .SetData(multiInvoiceData)
                    //.SetDelegationHash("{Put your DelegationHash}")
                    //.SetDelegatorId("{Put your DelegatorId}")
                    //.SetForceDelegation("{Put your ForceDelegatio}")
                    .Build();
billingService.IssueMultiInvoice(issueMultiInvoiceVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## کاهش فاکتور تسهیمی
در فاکتور تسهیمی نیز مانند فاکتور عادی با لغو شدن، کل مبلغ فاکتور و با کاهش، قسمتی از مبلغ به مشتری بازگردانده می شود. ولی در فاکتور تسهیمی برای کاهش لازم است کل سهم ها مجدداً اعلام شوند تا مبلغی که کسر می شود از حساب درست برداشته شود. برای کاهش فاکتور تسهیمی از سرویس ReduceMultiInvoice استفاده نمایید.
مقدار id در تمام بخش های اطلاعات ارسالی باید مطابق با شناسه های فاکتور اصلی باشد، در غیر این صورت خطا رخ می دهد. در فاکتور اصلاح شده نیز شرایط زیر لازم است برقرار باشد:      
the share of dealer + the share of shareholder =  the price to be payed by customer
```
 var output = new ResultSrv<InvoiceSrv>();
var mainInvoiceVos = ReduceInvoiceItemVo.ConcreteBuilder
                    .SetId({Put your Id})
                    .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                    {
                        ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                    })
                    .Build();

var subInvoiceVos = new List<ReduceInvoiceItemVo>
                {
                    ReduceInvoiceItemVo.ConcreteBuilder
                        .SetId({Put your Id})
                        .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                        {
                            ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your 
                            Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                        })
                        .Build()
                };
                var customerInvoiceItems = new List<ReduceInvoiceSubItemVo>
                {
                    ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity})
                        .Build()
                };

var reduceMultiInvoiceDataVo = ReduceMultiInvoiceDataVo.ConcreteBuilder
                    .SetMainInvoice(mainInvoiceVos)
                    .SetSubInvoices(subInvoiceVos)
                    .SetCustomerInvoiceItemVOs(customerInvoiceItems)
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    .Build();

var reduceMultiInvoiceVo = ReduceMultiInvoiceVo.ConcreteBuilder
                    .SetData(reduceMultiInvoiceDataVo)
                    .Build();
billingService.ReduceMultiInvoice(reduceMultiInvoiceVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## کاهش فاکتور تسهیمی و انتقال به شبا
در صورتی که می خواهید بلافاصله بعد از کاهش فاکتور، مبلغ برگشتی به شماره شبا کاربر منتقل گردد، از سرویس زیر با همان فرمت data سرویس ReduceMultiInvoice، استفاده نمایید.

```
var output = new ResultSrv<InvoiceSrv>();
var mainInvoiceVos = ReduceInvoiceItemVo.ConcreteBuilder
                    .SetId({Put your Id})
                    .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                    {
                        ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your 
                        Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                    })
                    .Build();

var subInvoiceVos = new List<ReduceInvoiceItemVo>
                {
                    ReduceInvoiceItemVo.ConcreteBuilder
                        .SetId({Put your Id})
                        .SetReduceInvoiceItemVOs(new List<ReduceInvoiceSubItemVo>
                        {
                            ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your Description}").SetPrice(50)
                                .SetQuantity({Put your Quantity}).Build()
                        })
                        .Build()
                };
                var customerInvoiceItems = new List<ReduceInvoiceSubItemVo>
                {
                    ReduceInvoiceSubItemVo.ConcreteBuilder.SetId({Put your Id}).SetDescription("{Put your 
                    Description}").SetPrice({Put your Price}).SetQuantity({Put your Quantity}).Build()
                };

var reduceMultiInvoiceDataVo = ReduceMultiInvoiceDataVo.ConcreteBuilder
                    .SetMainInvoice(mainInvoiceVos)
                    .SetSubInvoices(subInvoiceVos)
                    .SetCustomerInvoiceItemVOs(customerInvoiceItems)
                    //.SetPreferredTaxRate({Put your PreferredTaxRate})
                    .Build();

var reduceMultiInvoiceAndCashoutVo = ReduceMultiInvoiceAndCashoutVo.ConcreteBuilder
                    .SetData(reduceMultiInvoiceDataVo)
                    .SetToolCode({Put your ToolCode})
                    .Build();
billingService.ReduceMultiInvoiceAndCashout(reduceMultiInvoiceAndCashoutVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

### مجوز فروش محصول
همانطور که توضیح داده شد، به منظور صدور فاکتور تسهیمی (در صورت شراکت با یک کسب و کار دیگر)، فراخوانی سرویس nzh/biz/addDealer قبل از فراخوانی سرویس صدور فاکتور تسهیمی، الزامی ست. اما در صورتی که برای یک محصول خاص، بخواهید به کسب و کار دیگری مجوز صدور فاکتور عادی اعطا کنید، علاوه بر فراخوانی سرویس ذیل، باید سرویس nzh/biz/addDealer را نیز فراخوانی نمایید و سپس سرویس صدور فاکتور(nzh/issueInvoice) را  فراخوانی نمایید؛ در غیر این صورت با خطای  "کسب و کار دلال وارد شده دلال  کسب و کار مالک محصول نمی باشد" مواجه خواهید شد.
شناسه محصول(EntityId) و شناسه کسب و کار(DealerBizId) را کافی ست در در  کلاس AddDealerProductPermissionVo مقداردهی نمایید و سپس سرویس AddDealerProductPermission فراخوانی کنید.

```
var output = new ResultSrv<DealerProductPermissionSrv>();
var registerUserVo = AddDealerProductPermissionVo.ConcreteBuilder
                    .SetEntityId({Put your EntityId})
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.AddDealerProductPermission(registerUserVo, response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>
## دریافت لیست مجوزها
با این سرویس می توانید لیست مجوزهای خود به کسب و کارهای واسط دیگر را به انضمام شناسه محصول، مشاهده نمایید.

```
var output = new ResultSrv<List<DealerProductPermissionSrv>>();
var registerUserVo = DealerProductPermissionListVo.ConcreteBuilder
                    //.SetSize({Put your Size})
                    //.SetDealingBusinessId({Put your DealingBusinessId})
                    //.SetEnable({Put your Enable})
                    //.SetOffset({Put your Offset})
                    //.SetEntityId({Put your EntityId})
                    .Build();
billingService.DealerProductPermissionList(registerUserVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>

## لیست مجوزهای صادر شده برای کسب و کار شما
لیست دسترسی هایی که شما واسط آن کسب و کار شده اید و برای آن محصول خاص مجوز صدور فاکتور گرفته اید را می توانید با سرویس
زیر مشاهده نمایید.

```
var output = new ResultSrv<List<DealerProductPermissionSrv>>();
var registerUserVo = DealingProductPermissionListVo.ConcreteBuilder
                    //.SetSize({Put your Size})
                    //.SetDealingBusinessId({Put your DealingBusinessId})
                    //.SetEnable({Put your Enable})
                    //.SetOffset({Put your Offset})
                    //.SetEntityId({Put your EntityId})
                    .Build();
billingService.DealingProductPermissionList(registerUserVo,response => Listener.GetResult(response, out output));

```



<div class="box-end">
</div>
## فعال کردن دسترسی محصول
با استفاده از سرویس ذیل می توانید دسترسی محصولی به کسب و کار واسط اعطا نموده اید را فعال نمایید.

```
var output = new ResultSrv<DealerProductPermissionSrv>();
var enableDealerProductPermissionVo= EnableDealerProductPermissionVo.ConcreteBuilder
                    .SetEntityId({Put your EntityId})
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.EnableDealerProductPermission(enableDealerProductPermissionVo,response => Listener.GetResult(response, out output));
```<div class="box-end">
</div>
## غیرفعال کردن دسترسی محصول
 با استفاده از سرویس ذیل می توانید دسترسی محصولی که به کسب و کار واسط اعطا نموده اید را غیرفعال نمایید.

```
var output = new ResultSrv<DealerProductPermissionSrv>();
var registerUserVo = DisableDealerProductPermissionVo.ConcreteBuilder
                    .SetEntityId({Put your EntityId})
                    .SetDealerBizId({Put your DealerBizId})
                    .Build();
billingService.DisableDealerProductPermission(registerUserVo,response => Listener.GetResult(response, out output));
```



<div class="box-end">
</div>