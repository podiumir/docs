# فاکتور - نسخه‌ی PHP

[http://docs.pod.land/v1.0.8.0/Developer/Invoice/158/Index](http://docs.pod.land/vv.1.0.0.0/PODSDKs/PHPSDKs/2780/خرید در یک نگاه)
**نصب** **پکیج** **pod-billing-service**
پکیج ارائه شده برای  عملیات خرید، pod-billing-service، از طریق دستور زیر قابل نصب می باشد.

    composer require pod-sdk/pod-billing-service

## تنظیمات اولیه

قبل از استفاده از سرویس های خرید ابتدا با تنظیم serverType  مشخص کنید که در حالت تست هستید یا production  تا به سرور مورد نظر وصل شوید. همچنین  در تمام سرویس های خرید نیاز به تنظیم این دو پارامتر داریم : 

1. (توکنی که بعد از ورود به سیستم یا از پنل کسب و کار دریافت شده است و می توان به عنوان پارامتر هم وارد نمود) api_ token . 
2.  (مرجع صادرکننده توکن 0: توکن های داخلی (پیشفرض). 1: توکن های دریافت شده از sso) token_issuer.

با استفاده از کلاس baseInfo می توانید این سه پارامتر را تنظیم کنید:

    # required classes
    use Pod\Billing\Service\BillingService;
    use Pod\Base\Service\BaseInfo;
    use Pod\Base\Service\Exception\ValidationException;
    use Pod\Base\Service\Exception\PodException;
    
    const API_TOKEN = '{PUT API TOKEN}';
    const TOKEN_ISSUER = 1;
    # set serverType to BillingService::PRODUCTION_SERVER or BillingService::SANDBOX_SERVER
    putenv("SERVER_TYPE=". BillingService::PRODUCTION_SERVER);
    
    $baseInfo = new BaseInfo();
    $baseInfo->setToken(API_TOKEN);
    $baseInfo->setTokenIssuer(TOKEN_ISSUER);
    
    #  instantiates a BillingService
    $BillingService = new BillingService($baseInfo);

<div class="box-end">
</div>

## توکن یکبار مصرف

برای استفاده از برخی از API ها که تعداد دفعات اجرای آنها مهم است، لازم است پارامتر ott در هدر ارسال شود. این پارامتر در هر درخواست که به سرور ارسال می گردد تغییر می کند و ott جدید در پاسخ در خواست صادر می گردد.
اکثر عملیات مربوط به فاکتور نیاز به ott دارند که میتوانید آن را از آخرین درخواست به پلتفرم یا از طریق متد getOtt کلاس BillingService دریافت نمایید. فقط دقت نمایید که توکنی که با آن ott می گیرید با توکنی که در درخواست بعدی باید استفاده شود، یکی باشد. در کد زیر نمونه استفاده از این متد آورده شده است. 
مقدار ott را میتوانید از جواب سرویس issueInvoice هم دریافت نمایید و مجددا در سرویس صدور فاکتور فراخوانی نمایید.


    try {
        $result = $BillingService->getOtt();
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }

<div class="box-end">
</div>

## صدور فاکتور توسط کسب و کار
برای صدور فاکتور با استفاده از توکن کسب و کار از تابع issueInvoice استفاده کنید. شبه کد زیر یک فاکتور با دو بند فاکتور را شامل می شود:
دقت کنید برای هر بند فاکتور مقدارهای مربوط به هر محصول(شناسه محصول، قیمت، تعداد و توضیح هر محصول) را در آرایه ای جداگانه وارد کنید.
  
      $param =
            [
                ## ============================ *Required Parameters  =========================
                "productList"   	=> [
                    [
                        # شناسه محصول . در صورتی که بند فاکتور محصول مرتبط ندارد مقدار آن 0 وارد شود
                        "productId"         => "{put product id}",
                        # مبلغ بند فاکتور. برای استفاده از قیمت محصول وارد شده از مقدار auto استفاده نمایید
                        "price"             => "{put product price, type: decimal}",
                        #تعداد محصول
                        "quantity"          => "{put product price, type: integer}",
                        # توضیحات
                        "productDescription"=> "{put description}",
                    ],
                    // اطلاعات محصولات دیگر
                ],
                # کد صنف فاکتور
                "guildCode"			=> "{put guild code}", # *Required
    
                ## =========================== Optional Parameters  ===========================
                # توکن یک بار مصرف اگر وارد نشود در متد issueInvoice از api دریافت می شود
                "ott" 				=> "{put ott}",
                # آدرس فراخوانی صادر کننده فاکتور
                "redirectURL" 		=> "{put redirect uri}",
                # شناسه کاربر مربوط به مشتری برای بدست آورن این شناسه می توانید پروفایل کاربر را دریافت نمایید.
                "userId" 			=> "{put user id}",
                # شماره قبض
                "billNumber" 		=> "{put bill number}",
                # توضیحات فاکتور
                "description" 		=> "{put description}",
                # تاریخ سررسید شمسی yyyy/mm/dd
                "deadline" 			=> "yyyy/mm/dd",
                # کد ارز
                "currencyCode" 		=> "{put currency code like IRR}",  # default : IRR
                # شناسه یکی از آدرس های موجود کاربر
                "addressId" 		=> "{put address id of customer}",
                # لیست کد بن تخفیف
                "voucherHash" 		=> [],
                # نرخ مالیات برای این خرید که برای تمام آیتم های فاکتور اعمال می شود.
                #اگر مقداری ارسال نشود مقدار مالیات بر ارزش افزوده پیش فرض محاسبه می شود
                "preferredTaxRate" 	=> "{put tax, default 0.09}",
                # پرداخت دومرحله ای true/false
                "verificationNeeded"=> "{true/false}",
                # تایید خودکار فاکتور در پرداخت دومرحله ای true/false
                "verifyAfterTimeout"=> "{true/false}",
                # پیش نمایش فاکتور (در سیستم ثبت نمی گردد) true/false
                "preview" 			=> "{true/false}",
                # پرداخت فاکتور به روش امن
                "safe"				=> "{true/false}",
                # امکان اضافه کردن ووچر بعد از صدور فاکتور
                "postVoucherEnabled"=> "{true/false}",
                # آیا فاکتور رویداد دارد
                "hasEvent"			=> "{true/false}",
                # عنوان رویداد
                "eventTitle"		=> "{put event title}",
                # منطقه زمانی رویداد
                "eventTimeZone"		=> "{put event time zone}",
                # توضیحات رویداد
                "eventDescription"	=> "{put event description}",
                # متادیتا برای فاکتور
                "metadata"			=> '{put json format like {"name":"test"}}',
                #  اطلاعات جانبی رویداد format = json
                # example 1 : {bussinessName=’test’, bussinessURL=’www.test.com’, bussinessIcon=’null’,
                # actionList=[{command=’GET https://www.googleapis.com/calendar/v3/calendars/calendarId/events?privateExtendedProperty=petsAllowed%3Dyes
                # &sharedExtendedProperty=createdBy%3DmyApp’, commandType={code=’1’, value=’GET’}}], metaData={"petsAllowed":"yes"}}
                "eventMetadata"		=> [],
                # یادآورهای رویداد format = json
                # example 1 : {"id":0,"numOfDaysBefore":3,"alarmTime":1511789309821,"alarmType":"Email"}"
                # example 2 : {"id":0,"minute":15,"alarmType":"Notification"}
                "eventReminders"	=> [],
            ];
    
        try {
            $result = $BillingService->issueInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## نمایش پیش فاکتور
در پلتفرم کسب و کار، فاکتورهایی که پرداخت می شوند به صورت سالانه شماره سریال دریافت می نمایند، بنابرین کسب و کار می تواند برای امور مالی خود به آن شماره سریال استناد نماید. در برخی شرایط، ممکن است کسب و کار بخواهد  فاکتور تا زمانی که اقدام به پرداخت آن نشده اصلاً ثبت نگردد. بدین منظور با استفاده از سرویس زیر می تواند پیش فاکتور را ثبت نماید و با لینک بعدی آن را نمایش دهد. به محض اینکه مشتری، فاکتور را با کیف پول خود پرداخت  نماید یا برای پرداخت وارد درگاه بانکی شود، فاکتور ثبت می گردد. در صورتی  که مشتری پرداخت را از طریق درگاه لغو نماید یا اشکالی در پرداخت او به وجود آید، فاکتور به صورت خودکار لغو خواهد شد. 

 تابع createPreInvoice در پاسخ و در کلید preInvoiceUri یک url برای نمایش پیش فاکتور برمیگرداند که برای نمایش آن کاربر را به این صفحه هدایت کنید.
   
     $param = [
            ## ============================ *Required Parameters  =========================
            "ott"         => "bbfdcf363bec5774", # private-call-address توکن یک بار مصرف دریافتی از سرور
            "productList"   => [
                [
                    # شناسه محصول . در صورتی که بند فاکتور محصول مرتبط ندارد مقدار آن 0 وارد شود
                    "productId"         => "{put product id}",
                    # مبلغ بند فاکتور. برای استفاده از قیمت محصول وارد شده از مقدار auto استفاده نمایید
                    "price"             => "{put product price, type: decimal}",
                    #تعداد محصول
                    "quantity"          => "{put product price, type: integer}",
                    # توضیحات
                    "productDescription"=> "{put description}",
                ],
                //اطلاعات محصولات دیگر
            ],
            "guildCode"                 => "{put guild code}", # *			کد صنف فاکتور
            "redirectUri"               => "{put redirect uri}",
            "userId"               => "{put customer user id}",  # the id of customer
            ## =========================== Optional Parameters  ===========================
            # "billNumber"=> "{put bill numer}", #                              شماره قبض منحصر به فرد کسب و کار
            # "redirectUri" => "{put redrect uri}",
            #"callUrl"=>  "{put call uri}", #در صورت پرداخت موفق این آدرس صدا خواهد شد#
            # "preferredTaxRate" => "vat; default 0.09", # نرخ مالیات برای این خرید که برای تمام آیتم های فاکتور اعمال می شود.
            # "verificationNeeded" => "{true/false}",         # پرداخت دومرحله ای true/false
            # "currencyCode"=> "{put currency code}", #   کد ارز
            #  "description" => "{put description}", # توضیحات فاکتور
            # "deadline" => "yyyy/mm/dd",             # تاریخ سررسید شمسی yyyy/mm/dd
        ];
    
        try {
            $result = $BillingService->createPreInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
<div class="box-end">
</div>

## پرداخت فاکتور
1. پرداخت با کیف پول
تابع  getPayInvoiceByWalletLink لینک مشاهده فاکتور و پرداخت آن را تولید می‌کند. می توانید مشتری را به این آدرس برای پرداخت از طریق کیف پول و یا درگاه بانکی هدایت کنید.

      $param =
            [
                ## ============================ Required Parameters  =========================
                "invoiceId"     => "{put invoice id}",            # شناسه فاکتور
                ## ============================ Optional Parameters ==========================
                "redirectUri"   => "{put redirect uri}",
                "callUri"       => "{put call uri}",          # The function that will be called at the end of payment
            ];
    
        try {
            echo ($BillingService->getPayInvoiceByWalletLink($param)) . PHP_EOL;
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

2.  ‌پرداخت فاکتور خارج از پلتفرم پاد
با تابع issuInvoice می توانید پرداخت های غیر متعارف (خارج از پلتفرم) راکنترل کنید. به عنوان مثال اگر مبلغ فاکتور را به صورت حضوری از مشتری دریافت کردید می توانید با صدا زدن این تابع وضعیت فاکتور مورد نظر خود را به صورت پرداخت شده ببرید.

    $param =
        [
            ## ============================ *Required Parameters  =========================
            "invoiceId"     => "{put invoice id}",             # شناسه فاکتور
            ## =========================== Optional Parameters  ===========================
            "redirectUri"   => "{put redirect uri}",
            "callUri"       => "{put call uri}",
        ];
    try {
        $result = $BillingService->payInvoice($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }

3. پرداخت فاکتور با کیف پول از طریق پیامک
در صورتی که کاربر به رایانه جهت پرداخت دسترسی ندارد، یا در فروش حضوری، کسب و کار میتواند درخواست ارسال پیامک پرداخت به کاربر دهد و کاربر با پیامک کردن کدی که دریافت کرده به همان شماره، فاکتور را از کیف پول خود پرداخت مینماید.

    $param =
        [
            ## ============================ *Required Parameters  =========================
            "invoiceId"          => "{put invoice id}" , # شناسه فاکتور
            ## =========================== Optional Parameters  ===========================
            "wallet"             => "{put wallet code}",          # کد کیف پول PODLAND_WALLET
            "callbackUri"        => "{put call back uri}",         # آدرس جهت فراخوانی پس از پرداخت
            "redirectUri"        => "{put redirect uri}",          # آدرس جهت انتقال کاربر پس از پرداخت
            "delegationId"       => "{put delegation id}",        # شناسه اعتبار
            "forceDelegation"    => "{put force delegation}",   # پرداخت فقط از طریق اعتبار
        ];
    try {
        $result = $BillingService->sendInvoicePaymentSMS($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }

<div class="box-end">
</div>

## جستجو در متادیتای ثبت شده برای فاکتور
در هنگام ثبت فاکتور می توانید اطلاعات دلخواه خود را در کلید metadata  قرار دهید. در صورتی که بخواهید در بین متا دیتای فاکتورهای خود جستجو کنید می توانید از تابع  استفاده کنید.
   
     $param =
            [
                ## =========================== Optional Parameters  ===========================
                "metaQuery" =>  ["key"=>"value"],
                "offset" => "{put offset}",
                "size" => "{put size}",
                "isPayed" => "true/false",      # true/false
                "isCanceled" => "true/false",   # true/false
            ];
    
        try {
            $result = $BillingService->getInvoiceListByMetadata($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## دریافت فایل خروجی فاکتورها
از طریق تابع می توانید بر اساس پارامترهای مختلف فاکتورها را فیلتر کنید و از نتیجه حاصل یک فایل اکسل تولید کنید. خروجی این تابع دارای خصیصه id است که در ادامه برای دانلود فایل اکسل مورد نیاز است. ساخت فایل اکسل مدت زمانی طول می کشید و برای دریافت آن باید از تابع getExportList و id گرفته شده در این مرحله استفاده کرد.

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "guildCode" => "{put guild code}", # کد صنف
                "lastNRows" => "{put last n rows}", # n ردیف آخر فاکتور
                ## =========================== Optional Parameters  ===========================
                "id" => "{put invoice id}",
                "billNumber" => "{put bill number}", # شماره قبض که به تنهایی با آن می توان جستجو نمود
                "uniqueNumber" => "{put unique number}", # شماره کد شده ی قبض که به تنهایی با آن می توان جستجو نمود
                "trackerId" => "{put tracker id}",
                "fromDate" => "yyyy/mm/dd hh:mi:ss",          # تاریخ شمسی صدور فاکتور yyyy/mm/dd hh:mi:ss
                "toDate" => "yyyy/mm/dd hh:mi:ss",            # تاریخ شمسی صدور فاکتور yyyy/mm/dd hh:mi:ss
                "isCanceled" => "{true/false}",
                "isPayed" => "{true/false}",
                "isClosed" => "{true/false}",
                "isWaiting" => "{true/false}",
                "referenceNumber" => "{put reference number}",               # شماره ارجاع
                "userId" => "{put user id}",                          # شناسه کاربری مشتری
                "query" => "{put query}",                               # عبارت برای جستجو
                "productIdList" => [],  # لیست شماره محصولات
                "callbackUrl" => "{put call back url}",    # آدرس فراخوانی پس از اتمام تولید گزارش
            ];
        try {
            $result = $BillingService->getInvoiceListAsFile($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## تایید پرداخت فاکتور
اگر در هنگام صدور فاکتور کلید verificationNeeded را برابر با true قرار دهیم. فاکتور سه مرحله ایجاد شده و با استفاده از تابع verifyInvoice بعد از پرداخت فاکتور، می توانید پرداخت شدن آن را تایید کنید.   

     $param =
            [
                ## =========================== Optional Parameters  ===========================
                "id" => "{invoice id}",
                "billNumber" => "billNumber",
            ];
        try {
            $result = $BillingService->verifyInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
        
<div class="box-end">
</div>

## ابطال فاکتور
با استفاده از تابع cancelInvoice می توانید یک فاکتور را ابطال کنید.

       $param =
        [
            ## ============================ *Required Parameters  =========================
            "id" => "{put invoice id}", # شناسه فاکتور
        ];
    try {
        $result = $BillingService->cancelInvoice($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }

<div class="box-end">
</div>

## کاهش فاکتور
در مواردی ممکن است نیاز به تغییری در بندهای فاکتور داشته باشید. در  صورتی که فاکتور پرداخت نشده است، فاکتور قبلی را باطل (cancel) نمایید و فاکتور جدیدی صادر کنید. اگر فاکتور پرداخت شده است(در صورتی که باید پول بیشتری از مشتری دریافت نمایید)، لازم است فاکتوری جداگانه به مبلغ افزوده شده، با ذکر دلیل صادر نموده و مشتری را مجددا برای پرداخت هدایت نمایید. در برخی مواقع لازم است مبلغی از فاکتور پرداخت شده به مشتری بازگردانده شود. برای این منظور از  تابع reduceInvoice استفاده کنید.

   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "id" => "{put invoice id}", # شناسه فاکتور
                "invoiceItemList" => [
                    [
                        "invoiceItemId" => "{put invoice id of item 1}",    # شناسه بند فاکتور
                        "price" => "{put price of item 1}", # مبلغ بند فاکتور
                        "quantity" => "{put quantity of item 1}",  # لیست تعداد محصول در هر بند فاکتور
                        "itemDescription" => "reduce invoice", # لیست توضیحات بند فاکتور
                    ],
                    [
                        "invoiceItemId" => "{put invoice id of item 2}",    # شناسه بند فاکتور
                        "price" => "{put price of item 2}", # مبلغ بند فاکتور
                        "quantity" => "{put quantity of item 2}",  # لیست تعداد محصول در هر بند فاکتور
                        "itemDescription" => "reduce invoice", # لیست توضیحات بند فاکتور
                    ],
                ],
                ## =========================== Optional Parameters  ===========================
                "preferredTaxRate" => "{put tax, default 0.09}", # نرخ مالیات برای این خرید که برای تمام آیتم های فاکتور اعمال می شود. اگر مقداری ارسال نشود مقدار مالیات بر ارزش افزوده پیش فرض محاسبه می شود
            ];
        try {
            $result = $BillingService->reduceInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## تایید و بستن فاکتور در یک مرحله
اگر در هنگام صدور فاکتور کلید verificationNeeded را برابر با true قرار دهیم. فاکتور سه مرحله ایجاد شده و با استفاده از تابع verifyAndCloseInvoice بعد از پرداخت فاکتور، می توانید پرداخت شدن آن را تایید کنید و همزمان فاکتور را نیز ببندید.

      $param =
            [
                ## ============================ *Required Parameters  =========================
                "id" => "{put invoice id}" # شناسه فاکتور
                ## =========================== Optional Parameters  ===========================
            ];
        try {
            $result = $BillingService->verifyAndCloseInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
<div class="box-end">
</div>

## بستن فاکتور
با استفاده از تابع closeInvoice می توانید یک فاکتور را ببندید. دقت داشته باشید برای تسویه باید فاکتورها را بسته باشید.
  

      $param =
            [
                ## ============================ *Required Parameters  =========================
                "id" => "{put invoice id}", # شناسه فاکتور
            ];
        try {
            $result = $BillingService->closeInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
<div class="box-end">
</div>

## دریافت لینک پرداخت
با استفاده از تابع getInvoicePaymentLink می توانید لینک پرداخت یک فاکتور را دریافت کنید و کاربر را به این آدرس جهت پرداخت از طریق درگاه بانکی هدایت کنید.
   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "invoiceId"     => "{put invoice id}",                       # شناسه فاکتور
                ## ============================  Optional Parameters ==========================
                "redirectUri"   => "{put redirect uri}",
                "callbackUri"   => "{put callback uri}",      # The function that will be called at the end of payment
                "gateway"       => "PEP",
            ];
        try {
            $result = $BillingService->getInvoicePaymentLink($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## پرداخت فاکتور از طریق فاکتور
از طریق تابع این سرویس کسب و کار قادر خواهد بود که پرداخت شدن برخی فاکتورهای خود را منوط به پرداخت شدن فاکتورهای دیگری نماید. یا به عبارتی نوعی تهاتر را بوسیله فاکتورها انجام دهد. با استفاده از تابع payInvoiceByInvoice  می‌توانید این عملیات را انجام دهید.
   
     $param =
            [
                ## ============================ *Required Parameters  =========================
                "creditorInvoiceId" => "", # شناسه فاکتور بستانکار
                "debtorInvoiceId" => "", # شناسه فاکتور بدهکار
                ## =========================== Optional Parameters  ===========================
            ];
        try {
            $result = $BillingService->payInvoiceByInvoice($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## پرداخت فاکتور در آینده
از طریق تابع payInvoiceInFuture کسب و کار قادر خواهد بود فاکتورهایی که برایش توسط دیگران صادر شده را درتاریخ آینده یا سررسید توافقی از طریق مبلغی که در کیف پول یا اصناف خود دارد پرداخت نماید .این سرویس باید توسط کسب و کار یا کاربر بدهکار یا شخصی که فاکتور برایش صادر شده صدا زده شود.
   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "_ott_" => "" , # one time token - این توکن را در سرویس قبلی دریافت کرده اید.
                "invoiceId" => "{put invoice id}",                     # شناسه فاکتور
                "date" => "yyyy/mm/dd",# تاریخ شمسی سررسید
                ## =========================== Optional Parameters  ===========================
                # یکی و فقط یکی از فیلدهای زیر را باید پر کنید
                "guildCode" => "put guild code", # کد صنف
                "wallet" => "PODLAND_WALLET",  # کد کیف پول
            ];
        try {
            $result = $BillingService->payInvoiceInFuture($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
<div class="box-end">
</div>

## دریافت لینک دانلود فایل های اکسل فاکتورها
تابع getExportList لینک دانلود فایل های اکسل تولید شده را به شما خواهد داد. همچنین  با داشتن id ای که تابع getInvoiceListAsFile در خروجی می دهد می توانید تنها لینک دانلود فایل مورد نظر خود را استخراج کنید.
   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "offset" => "{put offset}",
                "size" => "{put size}",   # اندازه خروجی
                "id" => "{put request id}",  # شناسه درخواست
                ## =========================== Optional Parameters  ===========================
                "statusCode" => "{put status code}", # کد وضعیت
                "serviceUrl" => "{put server url}",           # آدرس سرویس
            ];
        try {
            $result = $BillingService->getExportList($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## پرداخت پیشرفته
کسب و کار میتواند برای تمام مشتریان خود، بدون نیاز به ورود به سامانه احراز هویت یکپارچه، امکان خرید را از طریق لینک پرداخت فراهم کند. برای این منظور لازم است کسب و کار از کد یکتا که برای فاکتور تولید می شود استفاده نماید. تابع getPayInvoiceByUniqueNumberLink لینک پرداخت را با استفاده از uniqueNumber تولید می کند.
   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "uniqueNumber"  => "{put unique number of invoice}",
                ## ============================  Optional Parameters ==========================
                "redirectUri"   => "{put redirect uri}",
                "callUri"       => "{put call uri}",          # The function that will be called at the end of payment
                "gateway"       => "PEP",
            ];
    
        try{
            echo ($BillingService->getPayInvoiceByUniqueNumberLink($param)).PHP_EOL;
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
        
[http://docs.pod.land/v1.0.8.0/Developer/Invoice/680/AdvancedPayment](http://docs.pod.land/vv.1.0.0.0/PODSDKs/PHPSDKs/2780/راهنمای مراحل پرداخت پیشرفته)


<div class="box-end">
</div> 

## درخواست تسویه
کسب و کار می تواند با استفاده از تابع requestWalletSettlement  درخواست انتقال وجه قابل تسویه موجود در حساب مجازی خود را بدهد. عملیات تسویه از طریق پنل نیز قابل انجام و پیگیری می باشد. همچنین میتوانید از طریق پنل کسب و کار خود یا وب سرویس برای یک حساب صنفی خاص یا کیف پول، تسویه  اتوماتیک را فعال نمایید. به این ترتیب پایان هر شب مبلغ قابل تسویه موجود در آن حساب، به شماره شبای ثبت شده واریز می گردد.

**تسویه از طریق پنل کسب و کار**
		تسویه از حساب مشتری (برداشت از کیف پول)
		تابع requestWalletSettlement انتقال پول از کیف پول به حساب بانکی را انجام می دهد. به عبارت دیگر مبلغ مورد نظر خود را با استفاده از این تابع می توانید از کیف پول خود به حساب بانکی منتقل کنید. در صورتی که شماره شبایا نام و نام خانوادگی شخص در پروفایل ثبت نشده باشد این سرویس خطا خواهد داد.
		  

      $param =
            [
                ## ============================ *Required Parameters  =========================
                "_ott_"         => "{Put ott here}" , # one time token - این توکن را در سرویس قبلی دریافت کرده اید.برای دریافت مجدد می توانید سرویس /nzh/ott/ را صدا کنید
                "amount"        => "{put amount}", # مبلغ برداشت
                ## =========================== Optional Parameters  ===========================
                "wallet"        => "{put wallet code}",          # کد کیف پول PODLAND_WALLET
                "firstName"     => "{put first name}",  # نام صاحب حسابی که تسویه به آن واریز می گردد
                "lastName"      => "{put last name}",  # نام خانوادگی صاحب حسابی که تسویه به آن واریز می گردد
                "sheba"         => "{put sheba}",  # شماره شبا حسابی که تسویه به آن واریز می گردد
                "currencyCode"  => "{put currency code}",  # کد ارز پیش فرض IRR
                "uniqueId"      => "{put unique id}",          # شناسه یکتا
                "description"   => "{put description}",          # شرح دلخواه
            ];
        try {
            $result = $BillingService->requestWalletSettlement($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

## تسویه از حساب صنفی کسب و کار
در حساب های صنفی همواره مبلغی به عنوان مبلغ قابل تسویه وجود دارد که شامل دارایی کسب و کار بجز فاکتورهای باز او یا فاکتورهایی که مبلغ آن ها هنوز واریز نشده است، می باشد. مبلغ قابل تسویه را می توانید از طریق تابع requestGuildSettlement تسویه کنید.
 

       $param =
            [
                ## ============================ *Required Parameters  =========================
                "_ott_"         => "{put ott}" , # one time token - این توکن را در سرویس قبلی دریافت کرده اید.برای دریافت مجدد می توانید سرویس /nzh/ott/ را صدا کنید
                "amount"        => "{put amount}",                      # مبلغ برداشت
                "guildCode"     => "{put guild code}",                # کد صنف
                ## =========================== Optional Parameters  ===========================
                "wallet"        => "{put wallet code}",           # کد کیف پول
                "firstName"     => "{put first name}",  # نام صاحب حسابی که تسویه به آن واریز می گردد
                "lastName"      => "{put last name}",  # نام خانوادگی صاحب حسابی که تسویه به آن واریز می گردد
                "sheba"         => "{put sheba}",  # شماره شبا حسابی که تسویه به آن واریز می گردد
                "currencyCode"  => "{put currency code}",  # کد ارز پیش فرض IRR
                "uniqueId"      => "{put unique id}",             # شناسه یکتا
                "description"   => "{put description}",           # شرح دلخواه
            ];
        try {
            $result = $BillingService->requestGuildSettlement($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

## انتقال وجه از حساب کسب و کاری به کارت بانکی (با کسر کارمزد) یا شماره شبا
کسب و کار می تواند با استفاده از سرویس زیر مبلغ مورد نظر خود را از حساب مجازی به یک شماره کارت یا یک شماره شبا بانکی منتقل نماید. بدیهی است که در صورت استفاده از ابزار کارت به کار، کارمزد بانکی از حساب کسب و کار کسرخواهد شد و در صورت استفاده از ابزار پایا، انتقال وجه در زمان مصوب بانک مرکزی انجام خواهد شد.
برای پارامتر toolCode از یکی از مقادیر زیر استفاده نمایید:
SETTLEMENT_TOOL_SATNA
SETTLEMENT_TOOL_PAYA
SETTLEMENT_TOOL_CARD
و به طور مثال، در صورتی که انتقال از طریق کارت را انتخاب نموده اید، در قسمت toolId شماره کارت مقصد را وارد نمایید و در غیر این صورت شماره شبا را وارد نمایید.
   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "_ott_"         => "{put ott}" , # one time token - این توکن را در سرویس قبلی دریافت کرده اید.برای دریافت مجدد می توانید سرویس /nzh/ott/ را صدا کنید
                "amount"        => "{put amount}",                       # مبلغ برداشت
                "guildCode"     => "{put guild code}",                    # کد صنف
                "toolId"        => "{put tool id}",           # شماره ابزاری که تسویه به آن واریز می گردد
                "toolCode"      => "{put tool code}",# نوع ابزار برای تسویه کارت به کارت،پایا،ساتنا
                # [SETTLEMENT_TOOL_SATNA | SETTLEMENT_TOOL_PAYA | SETTLEMENT_TOOL_CARD]
                ## =========================== Optional Parameters  ===========================
                "firstName"     => "{put first name}",  # نام صاحب حسابی که تسویه به آن واریز می گردد
                "lastName"      => "{put last name}",  # نام خانوادگی صاحب حسابی که تسویه به آن واریز می گردد
                "currencyCode"  => "{put currency code}",       # کد ارز پیش فرض IRR
                "uniqueId"      => "{put unique id}",          # شناسه یکتا
                "description"   => "{put description}",          # شرح دلخواه
            ];
        try {
            $result = $BillingService->requestSettlementByTool($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

## گزارش وضعیت تسویه
با استفاده از تابع listSettlements می توانید لیست تسویه حساب های خود را ببینید یا در میان آن ها جست و جو کنید.
  

      $param =
            [
                ## ============================ *Required Parameters  =========================
                "offset"        => "{put offset}",      # مبلغ برداشت
                "size"          => "{put size}",        # اندازه خروجی
                ## =========================== Optional Parameters  ===========================
                "statusCode"    => "",  # کد وضعیت درخواست SETTLEMENT_REQUESTED، SETTLEMENT_SENT ، SETTLEMENT_DONE
                "currencyCode"  => "",  # کد ارز پیش فرض IRR
                "fromAmount"    => "",  # حد پایین مبلغ درخواست شده
                "toAmount"      => "",  # حد بالای مبلغ درخواست شده
                "fromDate"      => "",  # حد پایین تاریخ درخواست شمسی yyyy/mm/dd
                "toDate"        => "",  # حد بالای تاریخ درخواست شمسی yyyy/mm/dd
                "uniqueId"      => "",          # شناسه یکتا
            ];
        try {
            $result = $BillingService->listSettlements($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

##فعالسازی تسویه خودکار
در صورتی که تسویه خودکار برای یک کسب و کار فعال شود، مبلغ قابل تسویه آن کسب و کار به طور خودکار، یکبار در شبانه روز به شماره شبای اعلام شده در پروفایل کسب و کار یا شماره شبای اعلامی در سرویس زیر، تسویه می گردد.  با تابع addAutoSettlement می توانید تسویه خودکار را بر روی هر کدام از حساب‌های صنفی خود فعال کنید.
 

       $param =
            [
                ## ============================ *Required Parameters  =========================
                "guildCode"     => "{put guild code}",              # کد صنف
                ## =========================== Optional Parameters  ===========================
                "firstName"     => "",  # نام صاحب حسابی که تسویه به آن واریز می گردد
                "lastName"      => "",  # نام خانوادگی صاحب حسابی که تسویه به آن واریز می گردد
                "currencyCode"  => "",  # کد ارز پیش فرض IRR
                "instant"       => "true/false",  # در صورت true بودن تسویه حساب خودکار فوری و در صورت false بودن تسویه حساب خودکار فعال می شود .
                "sheba"         => "",          # شماره شبا حسابی که تسویه به آن واریز می گردد
            ];
        try {
            $result = $BillingService->addAutoSettlement($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
## لغو تسویه خودکار
با استفاده از تابع removeAutoSettlement می توانید تسویه حساب خودکار را از روی هر کدام از حساب های صنفی غیر فعال کنید.
   

     $param =
            [
                ## ============================ *Required Parameters  =========================
                "guildCode"     => "{put guild code}",              # کد صنف
                ## =========================== Optional Parameters  ===========================
                "currencyCode"  => "{like USD or IRR}",  # کد ارز پیش فرض IRR
            ];
        try {
            $result = $BillingService->removeAutoSettlement($param);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
        

<div class="box-end">
</div>

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
