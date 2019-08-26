
# احراز هویت - زبان   PHP


# “SSO”

## نصب پکیج pod-sso-service

پکیج ارائه شده برای  سامانه ورود یکپارچه، pod-sso-service، از طریق دستور زیر قابل نصب می باشد.

    composer require pod-sdk/pod-sso-service

این پکیج شامل تمام api های لازم برای احرازهویت از طریق وب و از طریق دستگاه (با استفاده از رمز یکبار مصرف) می باشد 

متدهای ارائه شده  شامل موارد زیر می باشند : 

وب : 

1.  "getAccessToken"
2. " refreshAccessToken"
3.  "getTokenInfo"
4.  "revokeToken"

"OTP":  

1. " handshake"
2.  "SignatureAuthorize"
3. " getOtpScenario"
4.  "verifyOTP"
5.  "getAccessTokenByOtp"
6.  "getAccessTokenByOtpScenario"

در ادامه نمونه کدهایی برای استفاده از هر کدام از متدهای ذکر شده ارائه شده است.

این سامانه بر اساس استاندارد OAuth2.0 پیاده سازی شده است، بنابراین جهت استفاده از سرویس های پلتفرم بایستی بر اساس این استاندارد جهت ورود کاربران و دریافت توکن استفاده کنیم. روش کلی به این صورت است که برای ورود کاربر، وی را به صفحه ورود سرور SSO راهنمایی میکنیم و پس از ورود کاربر، کد مربوط به کاربر به آدرس تعریف شده توسط کسب و کار ارسال می گردد. سپس با ارسال کد دریافت شده به سرور sso توکن دسترسی کاربر در یافت می شود پس از دریافت توکن، میتوان از آن برای صدازدن سایر سرویس های پلتفرم استفاده نمود و یا اطلاعات پروفایل کاربر را دریافت و ویرایش نمود. 

راهنمای چگونگی دریافت کد در لینک زیر آورده شده است.

توجه : این کد در مدت کوتاهی منقضی میشود. بنابرین بلافاصله باید نسبت به دریافت access_token و refresh_token اقدام شود.

راهنمای دریافت کد

ار آنجایی که در تمام متدهای احراز هویت نیاز به ارسال اطلاعات client_id و client_secret می باشد از کلاس ClientInfo برای تنظیم این مقادیر استفاده شده است که به عنوان پارامتر ورودی به کلاس SSOService ارسال می شود. 

در زیر نمونه کد برای این تنظیمات آورده شده است:

    # required classes
    use Pod\Base\Service\Exception\PodException;
    use Pod\Base\Service\Exception\ValidationException;
    use Pod\Sso\Service\SSOService;
    use Pod\Base\Service\ClientInfo;

    const CLIENT_ID = 'YOUR_CLIENT_ID';
    const CLIENT_SECRET = 'YOUR_CLIENT_SECRET';
    const REDIRECT_URI = 'YOUR_REDIRECT_URI';
    const API_TOKEN = 'YOUR_API_TOKEN';

    $clientInfo = new ClientInfo();
    $clientInfo->setClientId(CLIENT_ID);
    $clientInfo->setClientSecret(CLIENT_SECRET);

    // for get Access Token and Refresh Access Token you need set redirect uri
    $clientInfo->setRedirectUri(REDIRECT_URI);

    #  instantiates a SSOService
    $SSOService = new SSOService($clientInfo);

راهنمای ورودی ها و هدر برای دریافت توکن دسترسی کاربر

<div class="box-end">
</div>


## دریافت توکن دسترسی کاربر

پس از دریافت کد برای دریافت توکن دسترسی کاربربا استفاده از نمونه کد زیر و با پر کردن پارامترهای ورودی می توانید توکن دسترسی کاربر را دریافت نمایید.

       $params = [
          "code" => "put code here" # use code that you receive in url
       ];

       try {
            $result = $SSOService->getAccessToken($params);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>


## بروزرسانی توکن دسترسی کاربر

پس از گذشت زمان expires_in ، توکن دسترسی کاربر منقضی می شود. با استفاده از refresh_token و تابع زیر، توکن معتبر جدید درخواست دهید.

     $params = [
            "refresh_token" => "put refresh token"
        ];

        try {
            $result = $SSOService->refreshAccessToken($params);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>


## ابطال توکن

ممکن است به هر دلیلی بخواهید دسترسی برنامه به اطلاعات حساب کاربر را از بین ببرید. برای این کار می توانید از ابطال توکن استفاده کنید.

    # set token and token_type_hint
        $params = [
            "token" => API_TOKEN,
            "token_type_hint" => "put token type to `refresh_token` or `access_token`",
        ];

        try {
            $result = $SSOService->revokeToken($params);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## دریافت اطلاعات توکن 

برای این که از صحت و اعتبار توکن کاربر خود مطلع شوید می توانید اطلاعات توکن مورد نظر را دریافت کنید.

    # set token and token_type_hint
        $params = [
            "token" => API_TOKEN,
            "token_type_hint" => "put token type to `refresh_token` or `access_token`",
        ];

        try {
            $result = $SSOService->getTokenInfo($params);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }


<div class="box-end">
</div>


# "OTP"


## ورود با OTP با سرور

جهت ایجاد امکان ورود با رمز یکبار مصرف (OTP) برای کاربران، در حالتی که کسب و کار دارای سرور امن و قابلیت ایجاد ارتباط با SSO پاد از طریق سرور خود باشد، این روش پیشنهاد می گردد.

لازم است از طریق سرور، به ازای هر شماره موبایل یا دستگاهی که میخواهد لاگین شود، اطلاعات دستگاه را با متد handshake به SSO معرفی نمایید و keyId دریافت کنید.

http://docs.pod.land/v1.0.8.0/Developer/User/1861/otpwithserver

<div class="box-end">
</div>

## فراخوانی سرویس Handshake سمت SSO

سرویس handshake به منظور معرفی دستگاه و هم‌چنین تفاهم بر روی پارامترهای امضای دیجیتال(شامل algorithm،keyId) فراخوانی می‌شود.برای فراخوانی این سرویس علاوه بر api_token و client_id که از پنل مدیریت کسب و کار قابل دریافت است، لازم است کلید عمومی کسب و کار به سیستم معرفی شده باشد.

     $params = [
        ## =========================================== *Required Parameters ============================================
        "api_token"             => API_TOKEN,
        "device_uid"            => 'put device unique id here',         # Device unique id ,maximum 255 character
        ## =========================================== *Optional Parameters ============================================
        "device_name"           => 'put device name here',
        "device_type"           => 'put device type here',
        "device_lat"            => 'put device latitude here',
        "device_lon"            => 'put device longitude here',
        "device_os"             => 'put device os here',
        "device_os_version"     => 'put device os version here',

    ];
    try {
        $result = $SSOService->handshake($params);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }

 <div class="box-end">
</div>

## درخواست دریافت کد OTP**:

 پس از دریافت  key_id از مرحله قبل و با استفاده از کلید خصوصی (private_key)  از متد زیر برای ساخت امضای دیجیتال و ارسال آن و همچنین دریافت کد OTP اقدام کنید. کد مورد نظر بر اساس مقدار فیلد identity  که می فرستید به کاربر مورد نظر از طریق پیامک یا ایمیل فرستاده می شود.

      $privateKey = file_get_contents('put your private key file name');
        $params = [
            ## =========================================== *Required Parameters ============================================
            "privateKey"                => $privateKey,
            "keyId"                     => 'put key id that you receive from handshake here',
    //          "algorithm"                 => OPENSSL_ALGO_SHA256,
            "identity"                  => 'put identity [mobile phone number or email address] here',
            "response_type"             => 'code', # code | token | id_token
            ## =========================================== *Optional Parameters ============================================
            "identityType"              => 'put PHONE  identity type [PHONE | EMAIL]',
            "loginAsUserId"             => 'put loginAsUserId',
            "state"                     => 'put state',
            "client_id"                 => 'put client_id',
            "redirect_uri"              => 'put redirect_uri',
            "callback_uri"              => 'put callback_uri',
            "scope"                     => 'put scope',
            "code_challenge"            => 'put code_challenge',
            "code_challenge_method"     => 'put code_challenge_method',
            "referrer"                  => 'put referrer',
            "referrerType"              => 'put referrerType',
    
        ];
        try {
            $result = $SSOService->signatureAuthorize($params);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## تایید کد OTP
پس از دریافت otp  کاربر باید آن را ارسال کند. از طریق کد زیر و با استفاده امضای دیجیتالی که در متد signatureAuthorize دریافت می کنید  برای تایید کد otp ارسالی از کاربر استفاده کنید :

      $params = [
            ## =========================================== *Required Parameters ============================================
            "keyId"                     => 'put key id that you received from handshake here',
            "signature"                 =>   $signature,
            "otp"                       => 'put otp that is received from user here',
            "identity"                  => 'put identity [phone or email] here',
        ];
    
        try {
            $result = $SSOService->verifyOTP($params);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }

<div class="box-end">
</div>

## دریافت توکن از سرور SSO

با استفاده از کد دریافتی از متد verifyOTP و ارسال آن از طریق متد getAccessTokenByOTP توکن دسترسی را از سرور SSO دریافت کنید: 

       $params = [
            "code" => "put code", # use code that you received after verify otp
        ];
    
        try {
            $result = $SSOService->getAccessTokenByOTP($params);
            print_r($result);
        } catch (ValidationException $e) {
            print_r($e->getResult());
            print_r($e->getErrorsAsArray());
        } catch (PodException $e) {
            print_r($e->getResult());
        }
        

<div class="box-end">
</div>
