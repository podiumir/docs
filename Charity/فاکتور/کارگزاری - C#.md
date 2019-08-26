
# کارگزاری - C#

 کسب‌و‌کار‌ها می‌تواند کسب‌و‌کارهای دیگری را که با آن‌ها همکاری دارند ثبت‌نام کنند. این امکان برای کارگزاران و کسب‌و‌کارهایی که به تسهیم درآمد نیاز دارند بسیار مفید است. همچنین کاربران می‌توانند کسب‌و‌کارها را دنبال کنند، به آن‌ها امتیاز دهند و در مورد آن‌ها نظر دهند تمامی این کارها با استفاده از توابع این ماژول انجام می‌شود. برای اطلاعات بیشتر به لینک [http://docs.pod.land/v1.0.8.0/Developer/Brokerage/683/AddUserAndBusiness](http://docs.pod.land/v1.0.8.0/Developer/Brokerage/683/AddUserAndBusiness) مراجعه کنید.


 **طریقه نصب :** از طریق Package Manager Console و دستورزیر پکیج مربوطه را نصب نمایید. برای دریافت آخرین نسخه پکیج لینک [https://www.nuget.org/packages/POD_Dealing](https://www.nuget.org/packages/POD_Dealing/) چک نمایید.

```
Install-Package POD_Dealing -Version 1.0.1
```


 <div class="box-end">
</div>

## فراخوانی متدها

 برای فراخونی هریک از متدها, باید یک شی از کلاس DealingService ایجاد کنید. برای استفاده از هر سرویس باید کلاس مربوط به آند سرویس مقداردهی کنید و ازبا استفاده از کلاس DealingService و شی ایجاد شده بعنوان ورودی سرویس مورد نظر,سرویس را اجرا کنید.

```
var dealingService=new DealingService();
```


 <div class="box-end">
</div>

## ثبت کسب و کار و کاربر

جدید کسب و کار میتواند با استفاده از سرویس زیر، کسب و کارهای دیگری را که با آنها همکاری دارد را ثبت نماید. این امکان برای کارگزاران و کسب و کارهایی که به تسهیم درآمد نیاز دارند بسیار مهم است. با این اقدام، همزمان با ثبت کسب و کار، پنل کاربری نیز ساخته می‌شود. ایمیل کسب و کار و شماره موبایلی که برای او ثبت می شود، برای مواقعی که لازم باشد خود آن کسب و کار در پنل مدیریتی خود وارد شود و برخی اقدامات را بر عهده بگیرد، ضروری است و صاحب کسب و کار میتواند با استفاده از آن رمز عبور خود را تعیین نماید. بنابراین صحت این موارد را کنترل نمایید. سرویس زیر عملیات مهم زیر را در یک عملیات انجام می دهد:

* 		با استفاده از نام کاربری و ایمیل و شماره موبایل که دریافت می کند، امکان ورود به پنل مدیریت کسب و کار برای کسب و کار دیگر فراهم می شود
* 		اطلاعات کسب و کار در پلتفرم (اصلی یا سندباکس) ثبت می شود
* 		یک اپلیکیشن (client) پیشفرض برای کسب و کار به صورت یکپارچه ایجاد می شود. که برای هر دو سرور سندباکس و اصلی اعتبار دارد
* 		بنابراین در صورتی که سرویس زیر را برای مثال در سندباکس فراخوانی نمودید، برای انتقال به سرور اصلی کافیست با همان توکنی که برای کسب و کار از سرور سندباکس دریافت نموده اید، اطلاعات پروفایل کاربر را در سرور اصلی دریافت نموده و یک کسب و کار برای آن کاربر ثبت نمایید.

در پاسخ سرویس بالا اطلاعات کسب و کار همراه با توکن دائمی آن، برگردانده می شود. ضروری است کارگزار توکن را ذخیره و برای اقداماتی که از جانب کسب و کار ثبت شده انجام می دهد استفاده نماید و در حفظ و امنیت آن کوشا باشد.

```
var output = new ResultSrv<BusinessSrv>();
var addUserAndBusinessVo = AddUserAndBusinessVo.ConcreteBuilder
                    .SetToken("{Put your ApiToken}")
                    .SetUsername("{Put your Username}")
                    .SetBusinessName("{Put your BusinessName}")
                    .SetGuildCode({Put your GuildCode})
                    .SetCountry("{Put your Country}")
                    .SetState("{Put your State}")
                    .SetCity("{Put your City}")
                    .SetAddress("{Put your Address}")
                    .SetDescription("{Put your Description}")
                    .SetAgentFirstName("{Put your AgentFirstName}")
                    .SetAgentLastName("{Put your AgentLastName}")
                    .SetEmail("{Put your Email}")
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetNationalCode("{Put your NationalCode}")
                    //.SetEconomicCode("{Put your EconomicCode}")
                    //.SetRegistrationNumber("{Put your RegistrationNumber}")
                    //.SetCellphone("{Put your Cellphone}")
                    //.SetPhone("{Put your Phone}")
                    //.SetFax("{Put your Fax}")
                    //.SetPostalCode("{Put your PostalCode}")
                    //.SetNewsReader({Put your NewsReader})
                    //.SetLogoImage("{Put your LogoImage}")
                    //.SetCoverImage("{Put your CoverImage}")
                    //.SetTags({Put your Tags}
                    //.SetTagTrees({Put your TagTrees})
                    //.SetTagTreeCategoryName("{Put your TagTreeCategoryName}")
                    //.SetLink("{Put your Link}")
                    //.SetLat({Put your Lat})
                    //.SetLng({Put your Lng})
                    //.SetAgentNationalCode("{Put your AgentNationalCode}")
                    .Build();
dealingService.AddUserAndBusiness(addUserAndBusinessVo, response => Listener.GetResult(response, out output));
```


 <div class="box-end">
</div>

## جستجو و ویرایش کسب و کارها

 برای دریافت لیست کسب و کارهایی که ایجاد نموده اید کافیست از سرویس زیر استفاده نمایید.

```
var output = new ResultSrv<List<BusinessSrv>>();
 var listUserCreatedBusinessVo = ListUserCreatedBusinessVo.ConcreteBuilder
                    .SetToken("{Put your Token}")
                    //.SetBizId({Put your BizId})
                    //.SetGuildCode({Put your GuildCode})
                    //.SetOffset({Put your Offset})
                    //.SetSize({Put your Size})
                    //.SetQuery("{Put your Query}")
                    //.SetTags({Put your Tags})
                    //.SetTagTrees({Put your TagTrees})
                    //.SetActive({Put your Active})
                    //.SetCountry("{Put your Country}")
                    //.SetState("{Put your State}")
                    //.SetCity("{Put your City}")
                    //.SetSsoId({Put your SsoId})
                    //.SetUsername("{Put your Username}")
                    //.SetBusinessName("{Put your BusinessName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetNationalCode("{Put your NationalCode}")
                    //.SetEconomicCode("{Put your EconomicCode}")
                    //.SetEmail("{Put your Email}")
                    //.SetCellphone("{Put your Cellphone}")
                    .Build();
dealingService.ListUserCreatedBusiness(listUserCreatedBusinessVo, response => Listener.GetResult(response, out output));
```


<div class="box-end">
</div>

## ویرایش کسب و کارها

برای ویرایش کسب و کارهایی که ایجاد نموده اید از سرویس زیر استفاده نمایید.

توجه داشته باشید، بجز موارد اجباری که عدم ثبت آنها منجر به خطا خواهد شد، عدم ارسال سایر موارد منجر به پاک شدن مقدار قبلی می گردد.

```
var output = new ResultSrv<BusinessSrv>();
var updateBusinessVo = UpdateBusinessVo.ConcreteBuilder
                    .SetToken("{Put your Token}")
                    .SetBizId({Put your BizId})
                    .SetBusinessName("{Put your BusinessName}")
                    .SetGuildCode({Put your GuildCode})
                    .SetCountry("{Put your Country}")
                    .SetState("{Put your State}")
                    .SetCity("{Put your City}")
                    .SetAddress("{Put your Address}")
                    .SetDescription("{Put your Description}")
                    //.SetCompanyName("{Put your CompanyName}")
                    //.SetShopName("{Put your ShopName}")
                    //.SetShopNameEn("{Put your ShopNameEn}")
                    //.SetWebsite("{Put your Website}")
                    //.SetDateEstablishing("{Put your DateEstablishing}")
                    //.SetFirstName("{Put your FirstName}")
                    //.SetLastName("{Put your LastName}")
                    //.SetSheba("{Put your Sheba}")
                    //.SetNationalCode("{Put your NationalCode}")
                    //.SetEconomicCode("{Put your EconomicCode}")
                    //.SetRegistrationNumber("{Put your RegistrationNumber}")
                    //.SetEmail("{Put your Email}")
                    //.SetCellphone("{Put your Cellphone}")
                    //.SetPhone("{Put your Phone}")
                    //.SetFax("{Put your Fax}")
                    //.SetPostalCode("{Put your PostalCode}")
                    //.SetChangeLogo({Put your ChangeLogo})
                    //.SetChangeCover({Put your ChangeCover})
                    //.SetLogoImage("{Put your LogoImage}")
                    //.SetCoverImage("{Put your CoverImage}")
                    //.SetTags({Put your Tags})
                    //.SetTagTrees({Put your TagTrees})
                    //.SetTagTreeCategoryName("{Put your TagTreeCategoryName}")
                    //.SetLink("{Put your Link}")
                    //.SetLat({Put your Lat})
                    //.SetLng({Put your Lng})
                    //.SetAgentFirstName("{Put your AgentFirstName}")
                    //.SetAgentLastName("{Put your AgentLastName}")
                    //.SetAgentCellphoneNumber("{Put your AgentCellphoneNumber}")
                    //.SetAgentNationalCode("{Put your AgentNationalCode}")
                    //.SetChangeAgent({Put your ChangeAgent})
                    .Build();
dealingService.UpdateBusiness(updateBusinessVo, response => Listener.GetResult(response, out output));
```


 <div class="box-end">
</div>

## دریافت توکن کسب و کار ایجاد شده

 هنگامی که با استفاده از توکن خود کسب و کارهایی را ثبت نمایید، به ازای هر کسب و کار یک apiToken برگردانده می شود که از آن جهت مدیریت امور کسب و کار زیر مجموعه میتوانید استفاده نمایید. در سایر مواقع که لیست کسب و کارهای ثبت شده را دریافت می نمایید این مقدار در لیست برگردانده نمی شود. در صورت نیاز به apiToken کسب و کار ایجاد شده میتوانید توسط سرویس زیر فقط برای یک کسب و کار به شرط اینکه قبلا خودتان آن را ایجاد کرده باشید، توکن کسب و کاری دریافت نمایید. دقت نمایید این توکن ها به مدت نامحدود فعال هستند و تا زمانی که revoke نشوند قابل استفاده می باشند. بنابرین مسائل امنیتی را در استفاده از آن در نظر بگیرید.

```
var output = new ResultSrv<BusinessApiTokenSrv>();
var getApiTokenForCreatedBusinessVo = GetApiTokenForCreatedBusinessVo.ConcreteBuilder
                    .SetToken("{Put your Token}")
                    .SetBusinessId({Put your BusinessId})
                    .Build();
dealingService.GetApiTokenForCreatedBusiness(getApiTokenForCreatedBusinessVo, response => Listener.GetResult(response, out output));
```


 <div class="box-end">
</div>

## امتیاز دهی به کسب و کار

کاربرانی که خرید موفق داشته باشند و دنبال کننده کسب و کار باشند، می توانند به کسب و کار مربوطه امتیاز دهند، برای ثبت امتیاز کسب و کار توکن دسترسی کاربر مورد نیاز است و از طریق سرویس زیر انجام می گیرد.در صورتی که کاربر کسب و کار را چندین بار امتیازدهی کند، آخرین امتیاز دهی جایگزین می گردد.

```
var output = new ResultSrv<RateSrv>();
var rateBusinessVo = RateBusinessVo.ConcreteBuilder
                    .SetToken("{Put your &#x64E;AccessToken}")
                    .SetBusinessId({Put your BusinessId})
                    .SetRate({Put your Rate})
                    .Build();
dealingService.RateBusiness(rateBusinessVo, response => Listener.GetResult(response, out output));
```


 <div class="box-end">
</div>

## ثبت نظر برای کسب و کار

 همچنین کاربران می توانند نظر خود را برای یک کسب و کار ثبت نمایند. برای این منظور از سرویس زیر و توکن دسترسی کاربر استفاده نمایید.علاوه بر آن، کسب و کار می تواند برای خودش نیز، نظر ثبت کند. 

 در پاسخ سرویس، شناسه نظر ثبت شده به عنوان result برگردانده می شود.

```
var output = new ResultSrv<long>();
var commentBusinessVo = CommentBusinessVo.ConcreteBuilder
                    .SetToken("{Put your AccessToken}")
                    .SetBusinessId({Put your BusinessId})
                    .SetText("{Put your Text}")
                    .Build();
dealingService.CommentBusiness(commentBusinessVo, response => Listener.GetResult(response, out output));
```


 <div class="box-end">
</div>

## افزودن کسب و کار به علاقه مندی ها

 با استفاده از سرویس زیر، کاربر می تواند کسب و کار را به لیست علاقمندی های خود اضافه کند.

```
 var output = new ResultSrv<bool>();
var businessFavoriteVo = BusinessFavoriteVo.ConcreteBuilder
                    .SetToken("{Put your &#x64E;AccessToken}")
                    .SetBusinessId({Put your BusinessId})
                    .SetDisFavorite({Put your DisFavorite})
                    .Build();
dealingService.BusinessFavorite(businessFavoriteVo, response => Listener.GetResult(response, out output));
```


 <div class="box-end">
</div>

## دریافت امتیاز کاربر نسبت به کسب و کار

 برای دریافت اطلاعات مربوط به تعاملات کاربر با کسب و کارها می توان از سرویس زیر استفاده نمود.
 در اینجا منظور از تعامل به عنوان مثال:
- آیا کاربر جاری کسب و کار را دنبال کرده است و یا خیر 
- کسب و کار جزء لیست علاقمندی کاربر می باشد یا خیر 
می باشد.

 اگر توکن کسب وکار را در کد زیر استفاده نمایید، rateCount مربوطه در نتیجه مربوط به تعداد امتیازدهی کاربران مختلف خواهد بود و اگر توکن کاربر لاگین شده را استفاده نمایید، rateCount همیشه برابر با یک خواهد بود. چرا که هر کاربر تنها یک بار قادر به امتیازدهی خواهد بود و با هر بار فراخوانی جدید سرویس امتیازدهی، امتیاز جدید جایگزین امتیاز قبلی خواهد شد و هم چنین مقدار rate برابر با میانگین امتیازهای ثبت شده می باشد که در صورت استفاده از توکن کاربر لاگین شده، مقدار عددی rate با myRate همیشه برابر خواهد بود.

```
var output = new ResultSrv<List<UserBusinessInfoSrv>>();
var userBusinessInfosVo = UserBusinessInfosVo.ConcreteBuilder
                    .SetToken("{Put your AccessToken Or ApiToken}")
                    .SetId({Put your Id})
                    .Build();
dealingService.UserBusinessInfos(userBusinessInfosVo, response => Listener.GetResult(response, out output));
```


<div class="box-end">
</div>

##  تایید یا رد نظرات از طرف کسب و کار

 با استفاده از سرویس زیر می توان نظرات را مشاهده نمود و سپس با استفاده از سرویس confirmComment نسبت به رد و یا تایید نظرات اقدام نمود. اگر فراخوانی سرویس با توکن لاگین شده کاربر صورت پذیرد، تنها نظرات کاربر را در نتیجه برمی گرداند و اگر توکن کسب وکار باشد، کل نظرات ثبت شده برای کسب و کار را نمایش خواهد داد.

```
var output = new ResultSrv<List<CommentSrv>>();
var commentBusinessListVo = CommentBusinessListVo.ConcreteBuilder
                    .SetToken("{Put your AccessToken Or ApiToken}")
                    .SetBusinessId({Put your BusinessId})
                    .SetSize({Put your Size})
                    .SetOffset({Put your Offset})
                    //.SetFirstId({Put your FirstId})
                    //.SetLastId({Put your LastId})
                    .Build();
dealingService.CommentBusinessList(commentBusinessListVo, response => Listener.GetResult(response, out output));
```


<div class="box-end">
</div>

## تایید یا عدم تایید نظرات

به منظور تایید و یا عدم تایید نظرات ثبت شده درسرویس CommentBusinessList، از سرویس زیر(ConfirmComment) استفاده نمایید.

```
var output = new ResultSrv<CommentSrv>();
var confirmCommentVo = ConfirmCommentVo.ConcreteBuilder
                    .SetToken("{Put your Token}")
                    .SetCommentId({Put your CommentId})
                    .Build();
dealingService.ConfirmComment(confirmCommentVo, response => Listener.GetResult(response, out output));
```

<div class="box-end">
</div>
