
# کارگزاری


[ابتدا jar فایل مربوطه را دانلود کرده و در پروژه خود قرار دهید.]

(https://github.com/FanapSoft/pod-java-sdk/tree/master/pod-dealing-service-java/Sample%20Code/release "ابتدا jar فایل مربوطه را دانلود کرده و در پروژه خود قرار دهید.")

## ثبت کسب و کار و کاربر جدید
 کسب و کار می‌تواند با استفاده از سرویس زیر، کسب و کارهای دیگری را که با آن‌ها همکاری دارد را ثبت نماید. این امکان برای کارگزاران و کسب و کارهایی که به تسهیم درآمد نیاز دارند بسیار مهم است. با این اقدام، همزمان با ثبت کسب و کار، پنل کاربری نیز ساخته می‌شود. ایمیل کسب و کار و شماره موبایلی که برای او ثبت می‌شود، برای مواقعی که لازم باشد خود آن کسب و کار در پنل مدیریتی خود وارد شود و برخی اقدامات را بر عهده بگیرد، ضروری است و صاحب کسب و کار می‌تواند با استفاده از آن رمز عبور خود را تعیین نماید. بنابراین صحت این موارد را کنترل نمایید. سرویس زیر عملیات مهم زیر را در یک عملیات انجام می‌دهد:

* 	با استفاده از نام کاربری و ایمیل و شماره موبایل که دریافت می‌کند، امکان ورود به پنل مدیریت کسب و کار برای کسب و کار دیگر فراهم می‌شود.
* 	اطلاعات کسب و کار در پلتفرم (اصلی یا سندباکس) ثبت می‌شود.
* 	یک اپلیکیشن (client) پیش‌فرض برای کسب و کار به صورت یکپارچه ایجاد می‌شود. که برای هر دو سرور سندباکس و اصلی اعتبار دارد.
* 	بنابراین در صورتی که سرویس زیر را برای مثال در سندباکس فراخوانی نمودید، برای انتقال به سرور اصلی کافیست با همان توکنی که برای کسب و کار از سرور سندباکس دریافت نموده اید، اطلاعات پروفایل کاربر را در سرور اصلی دریافت نموده و یک کسب و کار برای آن کاربر ثبت نمایید.

در پاسخ سرویس بالا اطلاعات کسب و کار همراه با توکن دائمی آن، برگردانده می‌شود. ضروری است کارگزار توکن را ذخیره و برای اقداماتی که از جانب کسب و کار ثبت شده انجام می‌دهد استفاده نماید و در حفظ و امنیت آن کوشا باشد.

```
  BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        List<String> permittedGuildCodeList = new ArrayList<>();
        permittedGuildCodeList.add({guild_code});

        try {
            AddUserAndBusinessVo addUserAndBusinessVo = new AddUserAndBusinessVo.Builder(baseInfoVo)
                    .setUsername({userName})
                    .setBusinessName("{businessName}")
                    .setEmail({email})
                    .setCountry({country})
                    .setState({state})
                    .setCity({city})
                    .setAddress({address})
                    .setDescription({description})
                    .setAgentFirstName({agent firstName})
                    .setAgentLastName({agent lastName})
                    .setAgentCellphoneNumber({agent cellphone})
                    .setGuildCode(permittedGuildCodeList )
                    .build();
            podDealing.addUserAndBusiness(addUserAndBusinessVo, new OnGetResponseListener<BusinessSrv>() {
                @Override
                public void onResponse(ResultVo<BusinessSrv> result) {
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


## دریافت لیست اصناف

جهت دریافت لیست اصناف از سرویس زیر استفاده نمایید.

```
    BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        try {
            GuildListVo guildListVo = new GuildListVo.Builder(baseInfoVo)
                    .setOffset({offset})
                    .setSize({size})
                    .build();
            podDealing.guildList(guildListVo, new OnGetResponseListener<List<GuildSrv>>() {
                @Override
                public void onResponse(ResultVo<List<GuildSrv>> result) {
                    System.out.println(result.getResult().get(2).getName());
                }

                @Override
                public void onFailed(PodException e) {
                    System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
                }
            });
        } catch (PodException e) {
            System.out.println("code : " + e.getCode() + "\nmessage : " + e.getMessage());
        }

    }
```

<div class="box-end">
</div>

## جستجو و ویرایش کسب و کارها
 
 برای دریافت لیست کسب و کارهایی که ایجاد نموده‌اید کافی‌است از سرویس زیر استفاده نمایید.
 
```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();
        List<Long> permittedBizIdList = new ArrayList<>();
        permittedBizIdList.add({biz id});
        PodDealing podDealing = new PodDealing();

        try {
            ListUserCreatedBusinessVo listUserCreatedBusinessVo = new ListUserCreatedBusinessVo.Builder(baseInfoVo)
                    .setSize({size})
                    .setOffset({offset})
                    .build();
            podDealing.listUserCreatedBusiness(listUserCreatedBusinessVo, new OnGetResponseListener<List<BusinessSrv>>() {
                @Override
                public void onResponse(ResultVo<List<BusinessSrv>> result) {
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

<div class="box-end">
</div>

## ویرایش کسب و کارها

برای ویرایش کسب و کارهایی که ایجاد نموده‌اید از سرویس زیر استفاده نمایید.

توجه داشته باشید، بجز موارد اجباری که عدم ثبت آن‌ها منجر به خطا خواهد شد، عدم ارسال سایر موارد منجر به پاک شدن مقدار قبلی می‌گردد.

```
  BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();
        List<String> permittedGuildCodeList = new ArrayList<>();
        permittedGuildCodeList.add({guild_code});
        PodDealing podDealing = new PodDealing();

        try {
            UpdateBusinessVo updateBusinessVo = new UpdateBusinessVo.Builder(baseInfoVo)
                    .setBizId({biz id})
                    .setBusinessName({businessName})
                    .setGuildCode(permittedGuildCodeList)
                    .setCountry({country})
                    .setState({state})
                    .setCity({city})
                    .setAddress({address})
                    .setDescription({description})
                    .build();
            podDealing.updateBusiness(updateBusinessVo, new OnGetResponseListener<BusinessSrv>() {
                @Override
                public void onResponse(ResultVo<BusinessSrv> result) {
                    System.out.println(result.getResult().getName());
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



## دریافت توکن کسب و کار ایجاد شده 

 هنگامی که با استفاده از توکن خود کسب و کارهایی را ثبت نمایید، به ازای هر کسب و کار یک apiToken برگردانده می‌شود که از آن جهت مدیریت امور کسب و کار زیر مجموعه می‌توانید استفاده نمایید. در سایر مواقع که لیست کسب و کارهای ثبت شده را دریافت می‌نمایید این مقدار در لیست برگردانده نمی‌شود. در صورت نیاز به apiToken کسب و کار ایجاد شده می‌توانید توسط سرویس زیر فقط برای یک کسب و کار به شرط این‌که قبلا خودتان آن را ایجاد کرده باشید، توکن کسب و کاری دریافت نمایید. دقت نمایید این توکن‌ها به مدت نامحدود فعال هستند و تا زمانی که revoke نشوند قابل استفاده می‌باشند. بنابرین مسائل امنیتی را در استفاده از آن در نظر بگیرید.


```
   BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        try {
            GetApiTokenForCreatedBusinessVo getApiTokenForCreatedBusinessVo = new GetApiTokenForCreatedBusinessVo.Builder(baseInfoVo)
                    .setBusinessId({businessId})

                    .build();
            podDealing.getApiTokenForCreatedBusiness(getApiTokenForCreatedBusinessVo, new OnGetResponseListener<BusinessApiTokenSrv>() {
                @Override
                public void onResponse(ResultVo<BusinessApiTokenSrv> result) {
                    System.out.println(result.getResult().getApiToken());
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

## امتیاز دهی به کسب و کار

 کاربرانی که خرید موفق داشته باشند و دنبال کننده کسب و کار باشند، می‌توانند به کسب و کار مربوطه امتیاز دهند، برای ثبت امتیاز کسب و کار توکن دسترسی کاربر مورد نیاز است و از طریق سرویس زیر انجام می‌گیرد.در صورتی که کاربر کسب و کار را چندین بار امتیازدهی کند، آخرین امتیاز دهی جایگزین می‌گردد.


```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        try {
            RateBusinessVo rateBusinessVo = new RateBusinessVo.Builder(baseInfoVo)
                    .setBusinessId({businessId})
                    .setRate({rate})

                    .build();
            podDealing.rateBusiness(rateBusinessVo, new OnGetResponseListener<RateSrv>() {
                @Override
                public void onResponse(ResultVo<RateSrv> result) {
                    System.out.println(result.getResult().getRate());
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

## ثبت نظر برای کسب و کار

 همچنین کاربران می‌توانند نظر خود را برای یک کسب و کار ثبت نمایند. برای این منظور از سرویس زیر و توکن دسترسی کاربر استفاده نمایید.علاوه بر آن، کسب و کار می‌تواند برای خودش نیز، نظر ثبت کند.  در پاسخ سرویس، شناسه نظر ثبت شده به عنوان result برگردانده می‌شود.


```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        try {
            CommentBusinessVo commentBusinessVo = new CommentBusinessVo.Builder(baseInfoVo)
                    .setBusinessId({businessId})
                    .setText({text})

                    .build();
            podDealing.commentBusiness(commentBusinessVo, new OnGetResponseListener<Long>() {
                @Override
                public void onResponse(ResultVo<Long> result) {
                    System.out.println(result.getMessageId());
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

## افزودن کسب و کار به علاقه مندی‌ها

 با استفاده از سرویس زیر، کاربر می‌تواند کسب و کار را به لیست علاقمندی‌های خود اضافه کند.


```
 BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        try {
            BusinessFavoriteVo businessFavoriteVo = new BusinessFavoriteVo.Builder(baseInfoVo)
                    .setBusinessId({businessId})
                    .setDisfavorite({true or false})

                    .build();
            podDealing.businessFavorite(businessFavoriteVo, new OnGetResponseListener<Boolean>() {
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

## دریافت امتیاز کاربر نسبت به کسب و کار

برای دریافت اطلاعات مربوط به تعاملات کاربر با کسب و کارها می‌توان از سرویس زیر استفاده نمود. در اینجا منظور از تعامل به عنوان مثال: امتیازی که کاربر به کسب وکار داده است آیا کاربر جاری کسب و کار را دنبال کرده است و یا خیر کسب و کار جزء لیست علاقمندی کاربر می‌باشد یا خیر اگر توکن کسب وکار را در کد زیر استفاده نمایید، rateCount مربوطه در نتیجه مربوط به تعداد امتیازدهی کاربران مختلف خواهد بود و اگر توکن کاربر لاگین شده را استفاده نمایید، rateCount همیشه برابر با یک خواهد بود. چرا که هر کاربر تنها یک بار قادر به امتیازدهی خواهد بود و با هر بار فراخوانی جدید سرویس امتیازدهی، امتیاز جدید جایگزین امتیاز قبلی خواهد شد و هم چنین مقدار rate برابر با میانگین امتیازهای ثبت شده می‌باشد که در صورت استفاده از توکن کاربر لاگین شده، مقدار عددی rate با myRate همیشه برابر خواهد بود.


```
   BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();
        List<Long> permittedIdList = new ArrayList<>();
        permittedIdList.add({id});
        PodDealing podDealing = new PodDealing();

        try {
            UserBusinessInfosVo userBusinessInfosVo = new UserBusinessInfosVo.Builder(baseInfoVo)
                    .setId(permittedIdList)

                    .build();
            podDealing.userBusinessInfos(userBusinessInfosVo, new OnGetResponseListener<List<UserBusinessInfoSrv>>() {
                @Override
                public void onResponse(ResultVo<List<UserBusinessInfoSrv>> result) {
                    System.out.println(result.getResult().get(0).getRate().getRate());
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

## تایید یا رد نظرات از طرف کسب و کار

 با استفاده از سرویس زیر می‌توان نظرات را مشاهده نمود و سپس با استفاده از سرویس confirmComment نسبت به رد و یا تایید نظرات اقدام نمود. اگر فراخوانی سرویس با توکن لاگین شده کاربر صورت پذیرد، تنها نظرات کاربر را در نتیجه برمی‌گرداند و اگر توکن کسب وکار باشد، کل نظرات ثبت شده برای کسب و کار را نمایش خواهد داد.


```
  BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        try {
            CommentBusinessListVo commentBusinessListVo = new CommentBusinessListVo.Builder(baseInfoVo)
                    .setBusinessId({businessId})
                    .setOffset({offset})
                    .setSize({size})
                    .build();
            podDealing.commentBusinessList(commentBusinessListVo, new OnGetResponseListener<List<CommentSrv>>() {
                @Override
                public void onResponse(ResultVo<List<CommentSrv>> result) {
                    System.out.println(result.getResult().get(0).getText());
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

## تایید یا عدم تایید نظرات

به منظور تایید و یا عدم تایید نظرات ثبت شده درسرویس CommentBusinessList، از سرویس زیر(ConfirmComment) استفاده نمایید.

```
   BaseInfoVo baseInfoVo = new BaseInfoVo.Builder()
                .setToken({token})
                .setToken_issuer(1)
                .setServerType(Enum_Server_type.PRODUCTION)
                .build();

        PodDealing podDealing = new PodDealing();

        try {
            ConfirmCommentVo confirmCommentVo = new ConfirmCommentVo.Builder(baseInfoVo)
                    .setCommentId({commentId})

                    .build();
            podDealing.confirmComment(confirmCommentVo, new OnGetResponseListener<Boolean>() {
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
