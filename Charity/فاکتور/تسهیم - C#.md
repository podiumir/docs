# تسهیم
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