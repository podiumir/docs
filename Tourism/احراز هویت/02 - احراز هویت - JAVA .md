# احراز هویت - زبان   Java

# "OTP"

ابتدا jar فایل مربوطه را دانلود کرده و در پروژه خود قرار دهید.

جهت ایجاد امکان ورود با رمز یکبار مصرف (OTP) برای کاربران، در حالتی که کسب و کار دارای سرور امن و قابلیت ایجاد ارتباط با SSO پاد از طریق سرور خود باشد، این روش پیشنهاد می گردد.

لازم است از طریق سرور، به ازای هر شماره موبایل یا دستگاهی که میخواهد لاگین شود، اطلاعات دستگاه را با متد handshake به SSO معرفی نمایید و keyId دریافت کنید.

<div class="box-end">
</div>

## فراخوانی سرویس handshake سمت SSO

سرویس handshake به منظور معرفی دستگاه و هم‌چنین تفاهم بر روی پارامترهای امضای دیجیتال (شامل algorithm،keyId) فراخوانی می‌شود.برای فراخوانی این سرویس نیاز به api_token و client_id می‌باشد که از پنل مدیریت کسب و کار قابل دریافت است.هم‌چنین لازم است قبل از فراخوانی، کلید عمومی کسب و کار به سیستم معرفی شده باشد:

تست و نمونه کد:

    SsoService ssoService = new SsoService();
            try {
                HandshakeVo handshakeVo = new HandshakeVo
                        .Builder()
                        .setAuthorization(API_KEY)
                        .setDevice_uid(SAMPLE_UID)
                        .setClient_id(CLIENT_ID)
                        .build();

                ssoService.handshake(handshakeVo, new OnGetResponseListenerHandshake() {
                    @Override
                    public void onResponse(HandshakeSrv handshakeSrv) {
                        System.out.println("KeyId: " + handshakeSrv.getKeyId());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

پارامتر **device_uid** توسط سرور کسب و کار تولید می‌شود و باید یک شناسه ی منحصر به فرد باشد.

زمان منقضی شدن کلید، یکسال می‌باشد.

در مرحله بعد لازم است با کلید دریافت شده و کلید خصوصی کسب و کار یک امضای دیجیتال تولید شود و همراه شماره موبایل کاربر به **SSO** ارسال گردد. 

<div class="box-end">
</div>

## ساخت signature

پس از دریافت **keyId** و **privateKey**، به روش زیر اقدام به ساخت امضای دیجیتال نمایید و مقدار امضای دیجیتال را در پارامتر **Authorization** قرار دهید.

پارامتر **Authorization** متشکل از سه بخش **Signature keyId** و **signature** و **headers** است:

_ **"Signature keyId"**:  مقدار دریافت شده شناسه کلید (**keyId**) از سرویس **handshake**.

_ **"signature"**:  ساخت **sign** به فرمت **base64** (توضیح نحوه ساخت در ادامه).

_ مقدار **headers**  دقیقا برابر با **host**  و یا **host date** می‌باشد.

Authorization=Signature keyId="keyId مقدار",signature="sign مقدار",headers="host"

ساخت **signature** مطابق با استاندارد **IETF: Signing HTTP Messages** و به روش زیر ساخته می‌شود.

اگر مقدار **headers** را برابر با **host** لحاظ نمودید، **host: accounts.pod.land** را به همراه مقدار **privateKey** با الگوریتم **RSA-SHA256** و به فرمت **base64** رمز نگاری نمایید.

و اگر مقدار **headers** را برابر با **host date** لحاظ نمودید، مقدار زیر را به همراه مقدار **privateKey** هش نمایید:

host: accounts.pod.land
date: Sat Jun 09 2018 17:47:37 GMT+0430

سپس رشته به دست آمده را در مقدار **signature** قرار دهید.

برای مشاهده یک مثال از نحوه ساخت **signature**، می‌توانید سایت https://accounts.pod.land/secTools.html را ببینید. همچنین می توانید از کلاس SigUtils که به زبان جاوا نوشته شده است استفاده نمایید.

<div class="box-end">
</div>

##  درخواست دریافت کد OTP

پارامتر **identity** می تواند حاوی شماره تلفن و یا ایمیل کاربر باشد.

پس از صدا زدن این سرویس، کد (رمز یکبار مصرف) به تلفن و یا ایمیل داده شده  ارسال می گردد. توجه داشته باشید رمز ارسال شده پس از 300 ثانیه منقضی می گردد.

پارامتر state اختیاری می باشد و در صورت ارسال، در پاسخ سرویس بعدی آن را دریافت خواهید کرد.

در پاسخ این سرویس شماره تلفن و یا ایمیل را در فیلد **identity** و شناسه کاربر را در فیلد **user_id** دریافت خواهید کرد. در صورتیکه کاربر جدید باشد **user_id** مقدار نخواهد داشت و پس از صدا زدن سرویس **verify** کاربر ثبت نام خواهد شد.

    SsoService ssoService = new SsoService();
            try {
                AuthorizeVo authorizeVo = new AuthorizeVo
                        .Builder()
                        .setResponse_type("code")
                        .setKeyId(SAMPLE_KEY_ID)
                        .setSignature(SAMPLE_SIGNATURE)
                        .setHeaders(SAMPLE_HEADER)
                        .setIdentity(SAMPLE_IDENTITY)
    //                .setReferrer("")
    //                .setReferrerType("")
    //                .setState("")
                        .build();

                ssoService.authorize(authorizeVo, new OnGetResponseListenerAuthorize() {
                    @Override
                    public void onResponse(AuthorizeSrv authorizeSrv) {
                        System.out.println("expire_in: " + authorizeSrv.getExpires_in() + "\n" +
                                "user_id: " + authorizeSrv.getUser_id());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

-توجه داشته باشید در اینجا، مقدار **user_id** برابر با **sso_id** واقعی(سمت core) است.

 **خطای رایج در سرویس فوق** 
اگر"identity" ارسال شده در سرویس، در سامانه پاد وریفای شده باشد (و یا به عبارت دیگر، متصل به userId) باشد، باید در مقدار پارامترclient_id ، شناسه مشتری متصل به همان "identity" فراخوانی شود؛ در غیر این صورت خطای Invalid client Id  را دریافت خواهید کرد.

**تایید otp** به شکل زیر است:

    SsoService ssoService = new SsoService();
            try {
                VerifyVo verifyVo = new VerifyVo
                        .Builder()
                        .setIdentity(SAMPLE_IDENTITY)
                        .setOtp("")
                        .setKeyId(SAMPLE_KEY_ID)
                        .setSignature(SAMPLE_SIGNATURE)
                        .setHeaders(SAMPLE_HEADER)
                        .build();

                ssoService.verify(verifyVo, new OnGetResponseListenerVerify() {
                    @Override
                    public void onResponse(VerifySrv verifySrv) {
                        System.out.println("code: " + verifySrv.getCode());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

در پاسخ سرویس فوق، پارامترهای code و state (در صورت وجود) را دریافت خواهید نمود.

**خطای رایج در سرویس فوق**: 
با ارسال کد اشتباه تا سه مرتبه، device  قفل خواهد شد و تا 15 دقیقه مجوز لاگین نخواهید داشت.
-در صورت ورود کد تایید درست و یا نادرست پیغام ورود موفق و ناموفق روی identity ارسالی دریافت خواهید نمود.

<div class="box-end">
</div>

## دریافت توکن از سرور SSO

برای دریافت توکن سرویس زیر را فراخوانی نمایید:

    SsoService ssoService = new SsoService();

            ClientInfoVo clientInfoVo = new ClientInfoVo();
            clientInfoVo.setClient_id(CLIENT_ID);
            clientInfoVo.setClient_secret(CLIENT_SECRET);

            try {
                GetAccessTokenByOtpVo getAccessTokenByOtpVo = new GetAccessTokenByOtpVo
                        .Builder()
                        .setClientInfoVo(clientInfoVo)
                        .setGrant_type(GRANT_TYPE)
                        .setCode("")
                        .build();

                ssoService.getAccessTokenByOtp(getAccessTokenByOtpVo, new OnGetResponseListenerGetAccessTokenOtp() {
                    @Override
                    public void onResponse(GetAccessTokenOtpSrv getAccessTokenOtpSrv) {
                        System.out.println("Access token: " + getAccessTokenOtpSrv.getAccess_token() + "\n" +
                                "Refresh token: " + getAccessTokenOtpSrv.getRefresh_token());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

پاسخ سرویس حاوی refresh_token، access_token و id_token می باشد که اعتبار access_token به مدت 15 دقیقه می باشد.

"Id_token" یک توکن self_encoded می باشد که فقط جهت شناسایی کاربر در مواقعی که بین چندین دستگاه جابجا می‌شود، استفاده می‌شود و برای دسترسی به api سرویس ها غیرقابل استفاده می باشد.

-"access_token" را به اپلیکیشن ارسال نمایید و توجه نمایید که refresh_token را سمت سرور نگه داری کرده و به اپلیکیشن ارسال ننمایید. ازrefresh_token  برای دریافت توکن جدید استفاده نمایید.

    SsoService ssoService = new SsoService();

            ClientInfoVo clientInfoVo = new ClientInfoVo();
            clientInfoVo.setClient_id(CLIENT_ID);
            clientInfoVo.setClient_secret(CLIENT_SECRET);

            try {
                RefreshAccessTokenVo refreshAccessTokenVo = new RefreshAccessTokenVo
                        .Builder()
                        .setClientInfoVo(clientInfoVo)
                        .setGrant_type("refresh_token")
                        .setRefresh_token("e5ded84ac41e479996c19932052f9605")
                        .build();

                ssoService.refreshAccessToken(refreshAccessTokenVo, new OnGetResponseListenerRefreshAccessToken() {
                    @Override
                    public void onResponse(RefreshAccessTokenSrv refreshAccessTokenSrv) {
                        System.out.println("Access token: " + refreshAccessTokenSrv.getAccess_token() + "\n" +
                                "Refresh token: " + refreshAccessTokenSrv.getRefresh_token());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

برای این قسمت دو سناریو در نظر گرفته شده است. در اولین سناریو ابتدا متد handshake و سپس متد authorize فراخوانی شده است:

    SsoService ssoService = new SsoService();

            try {
                HandshakeVo handshakeVo = new HandshakeVo
                        .Builder()
                        .setAuthorization(API_KEY)
                        .setDevice_uid(SAMPLE_UID)
                        .setClient_id(CLIENT_ID)
                        .build();

                ssoService.handshake(handshakeVo, new OnGetResponseListenerHandshake() {
                    @Override
                    public void onResponse(HandshakeSrv handshakeSrv) throws PodException {
                        SsoService ssoService = new SsoService();
                        AuthorizeVo authorizeVo = new AuthorizeVo
                                .Builder()
                                .setResponse_type("code")
                                .setKeyId(handshakeSrv.getKeyId())
                                .setSignature(SAMPLE_SIGNATURE)
                                .setHeaders(SAMPLE_HEADER)
                                .setIdentity(SAMPLE_IDENTITY)
    //                .setReferrer("")
    //                .setReferrerType("")
    //                .setState("")
                                .build();

                        ssoService.authorize(authorizeVo, new OnGetResponseListenerAuthorize() {
                            @Override
                            public void onResponse(AuthorizeSrv authorizeSrv) {
                                System.out.println("expire_in: " + authorizeSrv.getExpires_in() + "\n" +
                                        "user_id: " + authorizeSrv.getUser_id());
                            }

                            @Override
                            public void onFailed(PodException e) {
                                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                            }
                        });
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

در سناریوی دوم ابتدا متد verify و سپس متد getAccessTokenByOtp  فراخوانی شده است:

    SsoService ssoService = new SsoService();

            try {
                VerifyVo verifyVo = new VerifyVo
                        .Builder()
                        .setIdentity(SAMPLE_IDENTITY)
                        .setOtp(otp)
                        .setKeyId(SAMPLE_KEY_ID)
                        .setSignature(SAMPLE_SIGNATURE)
                        .setHeaders(SAMPLE_HEADER)
                        .build();

                ssoService.verify(verifyVo, new OnGetResponseListenerVerify() {
                    @Override
                    public void onResponse(VerifySrv verifySrv) throws PodException {
                        SsoService ssoService = new SsoService();

                        ClientInfoVo clientInfoVo = new ClientInfoVo();
                        clientInfoVo.setClient_id(CLIENT_ID);
                        clientInfoVo.setClient_secret(CLIENT_SECRET);

                        GetAccessTokenByOtpVo getAccessTokenByOtpVo = new GetAccessTokenByOtpVo
                                .Builder()
                                .setClientInfoVo(clientInfoVo)
                                .setGrant_type(GRANT_TYPE)
                                .setCode(verifySrv.getCode())
                                .build();

                        ssoService.getAccessTokenByOtp(getAccessTokenByOtpVo, new OnGetResponseListenerGetAccessTokenOtp() {
                            @Override
                            public void onResponse(GetAccessTokenOtpSrv getAccessTokenOtpSrv) {
                                System.out.println("Access token: " + getAccessTokenOtpSrv.getAccess_token() + "\n" +
                                        "Refresh token: " + getAccessTokenOtpSrv.getRefresh_token());
                            }

                            @Override
                            public void onFailed(PodException e) {
                                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                            }
                        });
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }
<div class="box-end">
</div>

# "SSO"

این سرور که جزئی از پلتفرم می باشد به عنوان سامانه احراز هویت مرکزی مورد استفاده قرار می گیرد. اکثر سرویس هایی که در ادامه معرفی می شوند باید دارای توکن معتبر از این سرور باشند.

همچنین کسب و کارها جهت تعریف کاربران جدید، دریافت و به روزرسانی پروفایل کاربران خود می توانند از این سرور استفاده نمایند و نیازی به نگهداری اطلاعات کاربران در سیستم خود ندارند.

این سامانه بر اساس استاندارد OAuth2.0  پیاده سازی شده است بنابراین جهت استفاده از سرویس های پلتفرم بایستی بر اساس این استاندارد جهت ورود کاربران و دریافت توکن استفاده نمایند.

روش کلی به این صورت است که برای ورود کاربر، وی را به صفحه ورود سرور SSO راهنمایی میکنیم و پس از ورود کاربر، توکن مربوط به کاربر به آدرس تعریف شده توسط کسب و کار ارسال می گردد. پس از دریافت توکن، میتوان از آن برای صدازدن سایر سرویس های پلتفرم استفاده نمود و یا اطلاعات پروفایل کاربر را دریافت و ویرایش نمود.
<div class="box-end">
</div>

## ‌ورود

برای ورود کاربران از طریق **SSO**  پاد از آدرس زیر استفاده کنید. مقدار client_id   خود را در آن قرار دهید و آدرسی که می خواهید پاسخ درخواست را در آن دریافت کنید را به عنوان پارامتر  redirect_uri ارسال نمایید.

 مقادیر **client_id** و **redirect_uri** باید منطبق بر کلید اتصال تعریف شده   توسط شما باشند.

    [sso-address]/oauth2/authorize/
       ?client_id=[CLIENT_ID]
        &response_type=[code]
        &redirect_uri=[REDIRECT_URI]
        &scope=profile

در صورت ورود موفق کاربر، پاسخ این درخواست در آدرس بازگشت به شکل زیر است:

دقت کنید که اگر به اسکوپ های درخواستی شما به هر دلیل اجازه دسترسی وجود نداشته باشد **Code**  خالی برگردانده می شود.

    ?code=[authorization_code]

این کد در مدت کوتاهی منقضی می شود. بنابرین بلافاصله باید نسبت به دریافت access_token و  refresh_token اقدام شود.

فهرست کامل پارامترهای این درخواست به شرح زیر است:

"**client_id**":  شناسه مشتری (اجباری)- دریافت این مقدار از پنل کسب و کار
"**response_type**":   نوع اطلاعات درخواستی - برای احراز هویت در اپلیکیشن های وب، از “code” استفاده نمایید و برای اپلیکیشن های موبایل از “token” یا “id_token” استفاده نمایید. 
"**redirect_uri**":  آدرس بازگشت- آدرس بازگشت ثبت شده برای وبسایت، مطابق با تنظیمات پنل کسب و کار
"**prompt**":  عملیات مورد نیاز-  می تواند login یا signup باشد. اگر ارسال نشود، روند عادی login طی می شود.
"**state**":  مقدار دلخواه که برنامه می خواهد در آدرس بازگشت، داشته باشد. 
"**scope**": شامل درخواست برنامه برای دسترسی به اطلاعات کاربر است- می تواند شامل یک یا چند مورد از موارد زیر باشد: profile ، email ، address ، activity ، legal، phone  مقدار پیش فرض profile:read می باشد و در صورت موافقت کاربر، توکنی که برای این scope صادر می شود فقط برای همان عملیات می تواند استفاده شود. Scope های بالا تنها اجازه خواندن اطلاعات کاربران را به شما می دهد. در صورت نیاز برای ویرایش اطلاعات کاربر :write را به انتهای اسکوپ اضافه نمایید. مثال: email:write  
"**code_challenge**": این پارامتر و پارامتر بعدی برای برنامه های بدون سرور استفاده می شوند.
"**code_challenge_method**":  متد رمز نگاری کد

\**توجــــه** تخصیص اسکوپ ها توسط تیم فنی انجام خواهد شد و اسکوپ های بیشتر باید توسط کسب و کار درخواست داده شود.

<div class="box-end">
</div>

## ‌دریافت توکن دسترسی کاربر

در صورتی که میخواهید کاربران شما از خدمات دیگر پلتفرم پایه مانند کیف پول استفاده نمایند، باید توکن دسترسی آنها را دریافت نمایید و با استفاده از آن، کاربر را در پلتفرم پایه ثبت نمایید. برای دریافت توکن دسترسی از درخواست زیر استفاده نمایید و علاوه بر client_secret و client_id و آدرس بازگشت، کد کاربر را نیز در آن قرار دهید.

    SsoService ssoService = new SsoService();

            ClientInfoVo clientInfoVo = new ClientInfoVo();
            clientInfoVo.setClient_id(CLIENT_ID);
            clientInfoVo.setClient_secret(CLIENT_SECRET);

            try {
                AccessTokenVo accessTokenVo = new AccessTokenVo
                        .Builder()
                        .setClientInfoVo(clientInfoVo)
                        .setGrant_type(GRANT_TYPE)
                        .setRedirect_uri(REDIRECT_URI)
                        .setCode("c5c8c7a4507b48e2b164d311e08494d0")
    //                .setCode_verifier("")
                        .build();
                ssoService.getAccessToken(accessTokenVo, new OnGetResponseListenerGetAccessToken() {
                    @Override
                    public void onResponse(GetAccessTokenSrv getAccessTokenSrv) {
                        System.out.println("Access token: " + getAccessTokenSrv.getAccess_token() + "\n" +
                                "Refresh token: " + getAccessTokenSrv.getRefresh_token());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

در این درخواست لازم است آدرس برگشت مطابق با   client_id و  client_secret و درست برابر با مقدار ارسال شده به صفحه ورود کاربران باشد. در غیر این صورت، خطای دسترسی اعلام خواهد شد.

پس از گذشت زمان expires_in ، توکن دسترسی کاربر منقضی می شود. با استفاده از refresh_token و درخواست زیر، توکن معتبر جدید درخواست دهید:

    SsoService ssoService = new SsoService();

            ClientInfoVo clientInfoVo = new ClientInfoVo();
            clientInfoVo.setClient_id(CLIENT_ID);
            clientInfoVo.setClient_secret(CLIENT_SECRET);

            try {
                RefreshAccessTokenVo refreshAccessTokenVo = new RefreshAccessTokenVo
                        .Builder()
                        .setClientInfoVo(clientInfoVo)
                        .setGrant_type("refresh_token")
                        .setRefresh_token("e5ded84ac41e479996c19932052f9605")
                        .build();

                ssoService.refreshAccessToken(refreshAccessTokenVo, new OnGetResponseListenerRefreshAccessToken() {
                    @Override
                    public void onResponse(RefreshAccessTokenSrv refreshAccessTokenSrv) {
                        System.out.println("Access token: " + refreshAccessTokenSrv.getAccess_token() + "\n" +
                                "Refresh token: " + refreshAccessTokenSrv.getRefresh_token());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }
<div class="box-end">
</div>

##  دریافت اطلاعات توکن‌

با استفاده از درخواست زیر می توانید از صحت و اعتبار توکن کاربر خود مطلع شوید.

    SsoService ssoService = new SsoService();

            ClientInfoVo clientInfoVo = new ClientInfoVo();
            clientInfoVo.setClient_id(CLIENT_ID);
            clientInfoVo.setClient_secret(CLIENT_SECRET);

            try {
                TokenInfoVo tokenInfoVo = new TokenInfoVo
                        .Builder()
                        .setClientInfoVo(clientInfoVo)
                        .setToken_type_hint("refresh_token")
                        .setToken("e5ded84ac41e479996c19932052f9605")
                        .build();

                ssoService.getTokenInfo(tokenInfoVo, new OnGetResponseListenerGetTokenInfo() {
                    @Override
                    public void onResponse(TokenInfoSrv tokenInfoSrv) {
                        System.out.println("Active state: " + tokenInfoSrv.isActive());
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

به عنوان **token_type_hint** سه مقدار مختلف قابل ارسال است که نوع توکن مورد نظر را مشخص می کند:

  \**"access_token ,  refresh_token  , id_token"**
<div class="box-end">
</div>

##  ابطال توکن

ممکن است به هر دلیلی بخواهید دسترسی برنامه به اطلاعات حساب کاربر را از بین ببرید. برای این منظور از درخواست زیر استفاده نمایید:

    SsoService ssoService = new SsoService();

            ClientInfoVo clientInfoVo = new ClientInfoVo();
            clientInfoVo.setClient_id(CLIENT_ID);
            clientInfoVo.setClient_secret(CLIENT_SECRET);

            try {
                RevokeTokenVo revokeTokenVo = new RevokeTokenVo
                        .Builder()
                        .setClientInfoVo(clientInfoVo)
                        .setToken_type_hint("refresh_token")
                        .setToken("e5ded84ac41e479996c19932052f9605")
                        .build();

                ssoService.revokeToken(revokeTokenVo, new OnGetResponseListenerRevokeToken() {

                    @Override
                    public void onResponse(Void result) {
                        System.out.println("code : 200" + "\nmessage : " + "The operation was successful");
                    }

                    @Override
                    public void onFailed(PodException e) {
                        System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                    }
                });
            } catch (PodException e) {
                System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
            }

<div class="box-end">
</div>
