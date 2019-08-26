
## تسهیم فروش
در صورتی که بخشی از فروش شما به کسب و کار دیگری تعلق دارد و می خواهید فاکتور به نام همان کسب و کار ثبت شود، لازم است آن کسب و کار، به کسب و کار شما اجازه صدور فاکتور به عنوان معامله گر را داده باشد. با در اختیار داشتن شناسه کسب و کار دیگر با استفاده از تابع  addDealer می توانید این اجازه را صادر کنید.


  

      $param =
            [
                ## ============================ *Required Parameters  =========================
                "dealerBizId"     => "{put dealer business id}",              # شناسه کسب و کار واسط
                ## =========================== Optional Parameters  ===========================
                "allProductAllow"  => true,             # دسترسی به همه محصولات
            ];
        try {
            $result = $BillingService->addDealer($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }


## لیست کسب و کارهایی که به آنها مجوز معامله داده شده 
برای دریافت یا جستجوی لیست تمام کسب و کارهایی که به آنها مجوز معامله و صدور فاکتور داده اید  می توانید از تابع dealerList استفاده کنید.
   

     $param =
            [
                ## =========================== Optional Parameters  ===========================
                'dealerBizId'   => "{put dealer business id}",            # The id of business to be a dealer
                'enable'        => true,            # [true/false]
                'size'          => "{put size}",              # pagination size, default: 50
                'offset'        => "{put offset}",               # pagination offset, default: 0
            ];
        try {
            $result = $BillingService->dealerList($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }


## فعالسازی و غیر فعالسازی مجوز معامله گران
با استفاده از تابع enableDealer می توانید کسب کارهای واسط را فعال کنید.
  

      $param =
            [
                ## ============================ *Required Parameters  =========================
                "dealerBizId"     => "{put dealer business id}",  # The id of dealer business *that is a number*
            ];
        try {
            $result = $BillingService->enableDealer($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

با استفاده از تابع disableDealer می توانید کسب کارهای واسط را غیر فعال کنید.
   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "dealerBizId"     => "{put business id}",  # The id of dealer business that is a number
            ];
        try {
            $result = $BillingService->disableDealer($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

## لیست کسب و کارهایی که واسط آن هستید
با فراخوانی سرویس businessDealingList می توانید لیست کسب و کارهایی که واسط آن ها شده اید را دریافت نمایید.

    $param =
   

     [
            ## =========================== Optional Parameters  ===============================
            'dealingBusinessId' => "{put dealer business id}",            # The id of dealing business
            'enable'            => true,            # [true/false]
            'size'              => "{put size}",              # pagination size, default: 50
            'offset'            => "{put offset}",               # pagination offset, default: 0
        ];
    try {
        $result = $BillingService->businessDealingList($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }

## صدور فاکتور تسهیمی
کسب و کار معامله گر که لازم است فاکتور تسهیمی صادر نماید باید از جانب کسب و کارهای سهیم دارای مجوز صدور فاکتور باشد. برای صدور فاکتور تسهیمی می توانید از متد issueMultiInvoice مشابه تابع زیر استفاده کنید:

   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "_ott_" => "put ott" ,                      # one time token - این توکن را در سرویس قبلی دریافت کرده اید.
                # آرایه حاوی اطلاعات فاکتورها
                "data" =>                       ## commented rows are optional parameters ##
                    [
                        // 'redirectURL' => 'put redirect url',
                        // 'userId' => 11111,               # userId of customer
                        // 'currencyCode' => 'like EUR or IRR',
                        // 'voucherHashs' => [],            # array of vouchers  اگر وجود ندارد این پارامتر ارسال نشود
                        // 'preferredTaxRate' => "{put tax, default 0.09}" ,     # tax to be added between 0 and 1 default is 0.09
                        // 'verificationNeeded' => 'true/false',
                        // 'preview' => '',
                        'mainInvoice'=>
                            [
                                // 'billNumber' => 'put bill number',       # business unique bill number
                                'guildCode' => 'put guild code',
                                // 'metadata' => 'extra data in form of json',
                                // 'description' => 'put description',
                                'invoiceItemVOs' =>
                                    [
                                        [
                                            'productId' => "{put product id or 0}",   # the id of product or 0 if no product
                                            'price' => "{put price}",     # the share of dealer
                                            'quantity' => "{put quantity}",    # count
                                            'description' => 'put description'
                                        ],
                                    ],
                            ],
                        'subInvoices' =>
                            [
                                [
                                    'businessId' => "{put business id}",       # the id of shareholder business
                                    'guildCode' => 'put guild code',
                                    // 'billNumber' => 'put bill number',       # business unique bill number
                                    // 'metadata' => 'extra data in form of json',
                                    'description' => 'put description',
                                    'invoiceItemVOs' =>
                                        [
                                            [
                                                'productId' => "{put product id or 0}",
                                                'price' => "{put price}",         # the share of shareholder
                                                'quantity' => "{put quantity}",
                                                'description' => 'put description'
                                            ],
                                        ],
                                ]
                            ],
                        // customerDescription => 'put customer description',
                        // customerMetadata => 'extra data for customer in form of json',
                        'customerInvoiceItemVOs' =>
                            [
                                [
                                    'productId' => "{put product id or 0}",       # the id of product or 0 if no product,
                                    'price' => "{put price}",         # the price to be payed by customer
                                    'quantity' => "{put quantity}",       # count
                                    'description' => 'put description'
                                ]
                            ]
                    ],
    
                ## =========================== Optional Parameters  ===============================
                'delegatorId'       => [],            # شناسه تفویض کنندگان، ترتیب اولویت را مشخص می کند
                'delegationHash'    => [],            # کد تفویض برای اشاره به یک تفویض مشخص
                'forceDelegation'   => false,              # پرداخت فقط از طریق تفویض
            ];
        try {
            $result = $BillingService->issueMultiInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

## کاهش فاکتور تسهیمی
همانند فاکتورهای عادی اگر نیاز به کاهش فاکتور و بر گردادن وجهی به مشتری باشد می توانید از تابع  reduceMultiInvoice استفاده کنید
 

    $param =
            [
                ## ============================ *Required Parameters  =========================
                # ***** NOTE : the share of dealer + the share of shareholder = the price to be payed by customer  **** #
                'data' =>
                    [
                        'preferredTaxRate' => "{put tax, default 0.09}",            # tax to be added between 0 and 1 default is 0.09
                        'mainInvoice' =>                             # فاکتور به نام خود معامله گر
                            [
                                'id' => "{put invoice id}",                # id of main invoice to be edited
                                'reduceInvoiceItemVOs' =>       # بندهای فاکتور مربوط به سهم معامله گر
                                    [
                                        [
                                            'id' => "{put invoice item id}",                 # the id of item in invoice
                                            'price' => "{put price}",                 # the share of dealer
                                            'quantity' => "{put quantity}",                # count
                                            'description' => 'put description of item'
                                        ]
                                    ]
                            ],
                        'subInvoices' =>            # فاکتورهای مربوط به سهم سایر کسب و کارهای ذینفع
                            [
                                [
                                    'id' => 222222,
                                    'reduceInvoiceItemVOs' =>       # بندهای فاکتور مربوط به سهم ذینفعان
                                        [
                                            [
                                                'id' => "{put invoice item id}",         # the id of item in invoice
                                                'price' => "{put price}",         # the share of shareholder
                                                'quantity' => "{put quantity}",        # count
                                                'description' => 'put description of item'
                                            ]
                                        ]
                                ]
                            ],
                        'customerInvoiceItemVOs' =>         # بندهایی که به مشتری نمایش داده می شوند
                            [
                                [
                                    'id' => "{put invoice item id}",         # the id of item in invoice
                                    'price' => "{put price}",         # he price to be payed by customer
                                    'quantity' => "{put quantity}",       # count
                                    'description' => 'put description of item'
                                ]
    
                            ],
                    ]
            ];
    
        try {
            $result = $BillingService->reduceMultiInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

 با استفاده از تابع reduceMultiInvoiceAndCacheOut علاوه بر کاهش فاکتور تسهیمی بلافاصله مبلغ برگشتی به شماره شبا کاربر منتقل گردد. ورودی و خروجی این تابع مشابه با تابع reduceInvoice است
 
        $param =
                        [
                            ## ============================ *Required Parameters  =========================
                            # ***** NOTE : the share of dealer + the share of shareholder = the price to be payed by customer  **** #
                            'data' =>
                                [
                                    'preferredTaxRate' => "{put tax, default 0.09}",            # tax to be added between 0 and 1 default is 0.09
                                    'mainInvoice' =>                             # فاکتور به نام خود معامله گر
                                        [
                                            'id' => "{put id of main invoice}",                # id of main invoice to be edited
                                            'reduceInvoiceItemVOs' =>       # بندهای فاکتور مربوط به سهم معامله گر
                                                [
                                                    [
                                                        'id' => "{put invoice item id}",                 # the id of item in invoice
                                                        'price' => "{put price}",                 # the share of dealer
                                                        'quantity' => "{put quantity}",                # count
                                                        'description' => 'put description of item'
                                                    ]
                                                ]
                                        ],
                                    'subInvoices' =>            # فاکتورهای مربوط به سهم سایر کسب و کارهای ذینفع
                                        [
                                            [
                                                'id' => 222222,
                                                'reduceInvoiceItemVOs' =>       # بندهای فاکتور مربوط به سهم ذینفعان
                                                    [
                                                        [
                                                            'id' => "{put invoice item id}",         # the id of item in invoice
                                                            'price' => "{put price}",         # the share of shareholder
                                                            'quantity' => "{put quantity}",        # count
                                                            'description' => 'put description of item'
                                                        ]
                                                    ]
                                            ]
                                        ],
                                    'customerInvoiceItemVOs' =>         # بندهایی که به مشتری نمایش داده می شوند
                                        [
                                            [
                                                'id' => "{put invoice item id}",         # the id of item in invoice
                                                'price' => "{put price}",         # he price to be payed by customer
                                                'quantity' => "{put quantity}",       # count
                                                'description' => 'put description of item'
                                            ]
                
                                        ],
                                ]
                        ];
                    try {
                        $result = $BillingService->reduceMultiInvoiceAndCashOut($param);
                        print_r($result);
                    } catch (ValidationException $e) {
                        print_r($e->getResult());
                        print_r($e->getErrorsAsArray());
                    } catch (PodException $e) {
                        print_r($e->getResult());
            


## مجوز فروش محصول
            با استفاده از تابع addDealerProductPermission به یک کسب و کار دیگر اجازه صدور فاکتور عادی را می توان داد
            
                $param =
                    [
                        ## =========================== Optional Parameters  ===============================
                        'productId'         => "{put product id}",            # شناسه محصول
                        'dealerBizId'       => "{put dealer business id}",            # شناسه کسب و کار واسط
                    ];
                try {
                    $result = $BillingService->addDealerProductPermission($param);
                    print_r($result);
                } catch (ValidationException $e) {
                    print_r($e->getResult());
                    print_r($e->getErrorsAsArray());
                } catch (PodException $e) {
                    print_r($e->getResult());
                }
 
  با استفاده از تابع dealerProductPermissionList می توانید لیست مجوزهای خود به کسب و کارهای واسط دیگر را به انضمام شناسه محصول مشاهد نمایید.

      $param =
                    [
                        ## =========================== Optional Parameters  ===============================
                        'productId'     => "{put product id}",                     # شناسه محصول
                        'dealerBizId'   => "{put dealer business id}",                     # شناسه کسب و کار واسط
                        'enable'        => "true/false",              # فعال بودن واسط
                        'offset'        => "{put offset}",                         # شناسه کسب و کار واسط
                        'size'          => "{put size}",                        # اندازه خروجی
            
            
                    ];
                try {
                    $result = $BillingService->dealerProductPermissionList($param);
                    print_r($result);
                } catch (ValidationException $e) {
                    print_r($e->getResult());
                    print_r($e->getErrorsAsArray());
                } catch (PodException $e) {
                    print_r($e->getResult());
                }
        

 هم چنین لیست دسترسی هایی که شما واسط آن کسب و کار شده اید و برای آن محصول خاص مجوز صدور فاکتور گرفته اید را می توانید با 
    سرویس dealingProductPermissionList  مشاهده نمایید.
    
        $param =
            [
                ## =========================== Optional Parameters  ==========================
                'productId'     => "{put product id}",                     # شناسه محصول
                'dealingBusinessId'   => "{put dealer business id}",                # شناسه کسب و کار واسط
                'enable'        => "true/false",              # فعال بودن واسط
                'offset'        => "{put offset}",                         # شناسه کسب و کار واسط
                'size'          => "{put size}",                        # اندازه خروجی
            ];
        try {
            $result = $BillingService->dealingProductPermissionList($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

## غیر فعال سازی دسترسی محصول برای کسب و کار
 با استفاده از تابع زیر می توانید دسترسی محصولی که به کسب و کار واسط اعطا نموده اید را غیرفعال نمایید

      $param =
            [
                ## ============================ *Required Parameters  =========================
                'productId'     => "{put product id}",               # شناسه محصول
                'dealerBizId'   => "{put dealer business id}",                # شناسه کسب و کار واسط
            ];
        try {
            $result = $BillingService->disableDealerProductPermission($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

## فعال سازی مجدد دسترسی محصول برای کسب و کار
با استفاده از تابع زیر می توانید دسترسی محصولی که به کسب و کار واسط اعطا نموده اید را در صورت غیر فعال بودن، مجدد فعال نمایید


    $param =
        [
            ## ============================ *Required Parameters  =========================
            'productId'     => "{put product id}",            # شناسه محصول
            'dealerBizId'   => "{put dealer business id}",                # شناسه کسب و کار واسط
    
    
        ];
    try {
        $result = $BillingService->enableDealerProductPermission($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }

<div class="box-end">
</div>
