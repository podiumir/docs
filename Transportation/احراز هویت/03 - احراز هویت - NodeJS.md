# احراز هویت - زبان   NodeJS

# “SSO”

برای کار با تمامی سرویس هایی پاد باید توکن دسترسی معتبر داشته باشید. همچنین کسب و کارها جهت تعریف کاربران جدید، دریافت و به روزرسانی پروفایل کاربران خود نیز می توانند از سرویس های پاد استفاده کنند که آن نیز مستلزم داشتن توکن معتبر است. تمامی کارهای دریافت و مدیریت توکن توسط ماژول SSO انجام می شود. این سامانه بر اساس استاندارد OAuth2.0 پیاده سازی شده است و دانستن این استاندارد می تواند کمک بسیاری به شما بکند.

از ماژول SSO می توانید برای ورود به دو روش وب و OTP (رمز یکبار مصرف استفاده کنید). همانطور که از نام آن مشخص است روش وب را در وب سایت ها استفاده می کنیم و از OTP اکثرا برای ورود با تلفن همراه استفاده می شود. نمونه کد های هر کدام از این دو مورد را می توانید در قسمت sample ماژول ببینید.

در روش وب، لینک ورود را مطابق با لینک زیر در وب سایت خود قرار دهید. توجه داشته باشید که client_id را می توانید در پنل کسب و کار خود پیدا کنید و آدرس بازگشت (redirect_uri) را نیز باید در این پل ثبت کنید و دقیقا همان آدرس را در این قسمت وارد کنید.

    https://accounts.pod.land/oauth2/authorize/
       ?client_id=[CLIENT_ID]
        &response_type=[code]
        &redirect_uri=[REDIRECT_URI]
        &scope=profile


**دریافت ماژول**

    npm install pod-sso-service


**ایجاد یک نمونه از ماژول:**

    const PodSSOService = require('pod-sso-service');
    let podSSOService = new PodSSOService({});;


**توابع:**
مربوط به وب:

1.  "getAccessToken
2. " refreshAccessToken
3.  "getTokenInfo
4.  "revokeToken

مربوط به OTP:

1. " handshake
2.  "Authorize
3.  "getOtpScenario
4.  "verify
5. " getAccessTokenByOtp
6.  "getAccessTokenByOtpScenario



<div class="box-end">
</div>

##  getAccessToken

 از این تابع برای گرفتن توکن دسترسی کاربر استفاده می شود. اعتبار این توکن محدود است (15 دقیقه) و باید در صورت نیاز با تابع refreshAccessToken به روز شود. پارامتر ورودی code به آدرس برگشت شما بعد از ورود کاربر از طریق لینک ورود پاد ارسال خواهد شد.

    let getAccessTokenData = {
      // ------ REQUIRED ------
      code: 'CODE',
      client_id: 'CLIENT ID',
      client_secret: 'CLIENT SECRET',
      redirect_uri: 'REDIRECT URI'
    
      // ------ OPTIONAL ------
      // grant_type: 'GRANT TYPE',
      // callback_uri: 'CALLBACK URI'
      // username: 'USERNAME'
      // identity: 'IDENTITY'
      // identityType: 'IDENTITY TYPE'
      // password: 'PASSWORD'
      // code_verifier: 'CODE VERIFIER'
    };
    
    podSSOService.getAccessToken(getAccessTokenData)
      .then(function (result) {
        console.log('function: getAccessToken ============>', result, '\n');
      })
      .catch(function (e) {
        console.log('error ============>', e);
      });


<div class="box-end">
</div>

##  refreshAccessToken
 
 به روز رسانی توکن دسترسی کاربر

     let refreshAccessTokenData = {
          // ------ REQUIRED ------
          refresh_token: 'REFRESH TOKEN',
          client_id: 'CLIENT ID',
          client_secret: 'CLIENT SECRET'
        
          // ------ OPTIONAL ------
          // grant_type: 'GRANT TYPE',
        };
        
        podSSOService.refreshAccessToken(refreshAccessTokenData)
          .then(function (result) {
            console.log('function: refreshAccessToken ============>', result, '\n');
          })
          .catch(function (e) {
            console.log('error ============>', e);
          });


<div class="box-end">
</div>

##  getTokenInfo

  گرفتن اطلاعات توکن

      let getTokenInfoData = {
          // ------ REQUIRED ------
          token: 'TOKEN',
          client_id: 'CLIENT ID',
          client_secret: 'CLIENT SECRET',
          token_type_hint: 'access_token | refresh_token | id_token'
        
          // ------ OPTIONAL ------
        };
        
        podSSOService.getTokenInfo(getTokenInfoData)
          .then(function (result) {
            console.log('function: getTokenInfo ============>', result, '\n');
          })
          .catch(function (e) {
            console.log('error ============>', e);
          });


<div class="box-end">
</div>

## revokeToken
 ابطال توکن

     let revokeTokenData = {
          // ------ REQUIRED ------
          token: 'TOKEN',
          client_id: 'CLIENT ID',
          client_secret: 'CLIENT SECRET',
          token_type_hint: 'access_token | refresh_token | id_token'
        
          // ------ OPTIONAL ------
        };
        
        podSSOService.revokeToken(revokeTokenData)
          .then(function (result) {
            console.log('function: revokeToken ============>', result, '\n');
          })
          .catch(function (e) {
            console.log('error ============>', e);
          });


<div class="box-end">
</div>

# OTP

## handshake

 جهت ایجاد امکان ورود با رمز یکبار مصرف (OTP) برای کاربران از این تابع استفاده می شود. برای آگاهی از جزییات روند رود با رمز یکبار مصرف به لینک زیر مراجعه کنید. همچنین دقت داشته باشید که برای استفاده از روش رمز یمبار مصرف باید کلید های عمومی و خصوصی خود را ایجاد کرده باشید و کلید عمومی را در پنل کسب و کار وارد کرده باشید:

راهنما

    let handshakeData = {
      // ------ REQUIRED ------
      device_uid: 'DEVICE UNIQUE ID',
      token: 'API TOKEN',
      client_id: 'CLIENT ID'
    
      // ------ OPTIONAL ------
      // device_lat: ''DEVICE LAT',
      // device_lon: ''DEVICE LON',
      // device_os: 'DEVICE OS',
      // device_os_version: 'DEVICE OS VERSION'
      // device_type: 'DEVICE TYPE',
      // device_name: 'DEVICE NAME',
      // algorithm: 'ALGORITHM'
    };
    
    podSSOService.handshake(handshakeData)
      .then(function (result) {
        console.log('function: handshake ============>', result, '\n');
      })
      .catch(function (e) {
        console.log('error ============>', e);
      });


<div class="box-end">
</div>

## authorize

  بعد از عملیات handshake می توانید با استفاده از این تابع به شماره موبایل یا ایمیل کاربر رمز یکبار مصرف را ارسال کنید. مقدار کلید authorization را باید با توجه به مستندات لینک زیر ایجاد کنید:

راهنما

    let authorizeData = {
      // ------ REQUIRED ------
      authorization: 'AUTHORIZATION HEADER',
      identity: 'MOBILE or EMAIL'
    
      // ------ OPTIONAL ------
      // response_type: 'RESPONSE TYPE'
      // identityType: 'IDENTITY TYPE',
      // loginAsUserId: 'LOGIN AS USER ID',
      // state: 'STATE',
      // redirect_uri: 'REDIRECT URI',
      // callback_uri: 'CALLBACK URI',
      // scope: 'SCOPE',
      // code_challenge: 'CODE CHALLENGE',
      // code_challenge_method: 'CODE CHALLENGE METHOD'
      // referrer: 'REFERRER',
      // referrerType: 'REFERRER TYPE'
    };
    
    podSSOService.authorize(authorizeData)
      .then(function (result) {
        console.log('function: handshake ============>', result, '\n');
      })
      .catch(function (e) {
        console.log('error ============>', e);
      });


<div class="box-end">
</div>

##  getOtpScenario

  این تابع کار هر دو تابع handshake و authorize را همزمان انجام داده و شما درگیر ایجاد sign نخواهید شد

    let getOtpScenarioData = {
      // ------ REQUIRED ------
      device_uid: 'DEVICE UNIQUE ID',
      identity: 'MOBILE or EMAIL',
      privateKey: 'PRIVATE KEY',
      token: 'API TOKEN',
      client_id: 'CLIENT ID'
    
      // ------ OPTIONAL ------
      // device_lon: 'DEVICE LON',
      // device_lat: 'DEVICE LAT',
      // device_os: 'DEVICE OS',
      // device_os_version: 'DEVICE OS VERSION'
      // device_type: 'DEVICE TYPE',
      // device_name: 'DEVICE NAME',
      // algorithm: 'ALGORITHM',
      // identityType: 'IDENTITY TYPE',
      // loginAsUserId: 'LOGIN AS USER ID',
      // state: 'STATE',
      // redirect_uri: 'REDIRECT URI',
      // callback_uri: 'CALLBACK URI',
      // scope: 'SCOPE',
      // code_challenge: 'CODE CHALLENGE',
      // code_challenge_method: 'CODE CHALLENGE METHOD'
      // referrer: 'REFERRE',
      // referrerType: 'REFERRER TYPE'
    };
    
    podSSOService.getOtpScenario(getOtpScenarioData)
      .then(function (result) {
        console.log('function: getOtpScenario ============>', result, '\n');
      })
      .catch(function (e) {
        console.log('error ============>', e);
      });


<div class="box-end">
</div>

## verify

  این تابع کد پیامک شده یا ایمیل شده به کاربر را (پارامتر otp) به سرور ارسال می کنید و در صورت صحت اطلاعات ارسالی کد مورد نیاز برای ورود را دریافت خواهید کرد. مقدار کلید authorization را می توانید خود تولید کنید اما اگر در مرحله قبلی از تابع getOtpScenario سناریو استفاده کرده باشید این مقدار در خروجی تابع در اختیار شما قرار می گیرد.
   
       let verifyData = {
              // ------ REQUIRED ------
              identity: 'MOBILE or Email',
              otp: 'CODE RECIEVED',
              authorization: 'Signature keyId=KEY ID,signature= SIGNATURE,headers=host'
            
              // ------ OPTIONAL ------
            };
            
            podSSOService.verify(verifyData)
              .then(function (result) {
                console.log('function: verify ============>', result, '\n');
              })
              .catch(function (e) {
                console.log('error ============>', e.code, e.message);
              });


<div class="box-end">
</div>

## getAccessTokenByOtp

  برای دریافت توکن دسترسی در حالت ورود با رمز یکبار مصرف از این تابع استفاده می شود.  پارامتر ورودی کد از خروجی تابع verify دریافت می شود.


    let getAccessTokenByOtpData = {
      // ------ REQUIRED ------
      code: 'CODE',
      client_id: 'CLIENT ID',
      client_secret: 'CLIENT SECRET'
    
      // ------ OPTIONAL ------
      // grant_type: 'GRANT TYPE',
    };
    
    podSSOService.getAccessTokenByOtp(getAccessTokenByOtpData)
      .then(function (result) {
        console.log('function: getAccessTokenByOtp ============>', result, '\n');
      })
      .catch(function (e) {
        console.log('error ============>', e.code, e.message);
      });


<div class="box-end">
</div>

## getAccessTokenByOtpScenario

 این تابع کار هر دو تابع verify و getAccessTokenByOtp همزمان انجام می دهد و توکن دسترسی را بر می گرداند.


    let getAccessTokenByOtpScenarioData = {
      // ------ REQUIRED ------
      identity: 'MOBILE or Email',
      otp: 'OTP',
      authorization: 'Signature keyId=KEY ID,signature= SIGNATURE,headers=host',
      client_id: 'CLIENT ID',
      client_secret: 'CLIENT SECRET'
    
      // ------ OPTIONAL ------
      // grant_type: 'GRANT TYPE'
    };
    
    podSSOService.getAccessTokenByOtpScenario(getAccessTokenByOtpScenarioData)
      .then(function (result) {
        console.log('function: getAccessTokenByOtpScenario ============>', result, '\n');
      })
      .catch(function (e) {
        console.log('error ============>', e.code, e.message);
      });

<div class="box-end">
</div>

