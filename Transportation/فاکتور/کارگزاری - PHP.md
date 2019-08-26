# کارگزاری

کسب و کار ها می‌توانند کسب و کارهای دیگری را که با آن ها همکاری دارند ثبت نام کنند. این امکان برای کارگزاران و کسب و کارهایی که به تسهیم درآمد نیاز دارند بسیار مفید است. همچنین کاربران می‌توانند کسب‌و‌کارها را دنبال کنند، به آن‌ها امتیاز دهند و در مورد آن‌ها نظر دهند تمامی این کارها با استفاده از توابع این پکیج انجام می‌شود.

برای اطلاعات بیشتر به لینک زیر مراجعه کنید
[راهنما](http://docs.pod.land/v1.0.8.0/Developer/Brokerage/683/AddUserAndBusiness "راهنما")

**نصب** **پکیج** **pod-dealing-service**

برای نصب پکیج pod-dealing-service کافیست دستور زیر را در روت اصلی برنامه اجرا کنید.

```

composer require pod-dealing-service
```


در ادامه توضیحات و نمونه کدهای استفاده از متدهای کلاس DealingService آورده شده است:

ابتدا کدهای مشترک قابل استفاده برای هریک از متد ها را مشاهده می کنید.

```

# required classes
use Pod\Dealing\Service\DealingService;
use Pod\Base\Service\Exception\ValidationException;
use Pod\Base\Service\Exception\PodException;

# set serverType to DealingService::PRODUCTION_SERVER or DealingService::SANDBOX_SERVER
putenv("SERVER_TYPE=". DealingService::PRODUCTION_SERVER);
const API_TOKEN = '{PUT API TOKEN}';
# access token will be expired each 15 minutes refresh this token with SSOService->refreshAccessToken
const ACCESS_TOKEN = '{PUT ACCESS TOKEN}';
const TOKEN_ISSUER = 1;

#  instantiates a DealingService
$dealingService = new DealingService();
```


<div class="box-end">
</div>

## ثبت کسب و کار و کاربر جدید

با استفاده از تابع addUserAndBusiness می توانید یک کسب و کار ثبت کنید. با این اقدام، همزمان با ثبت کسب و کار، پنل کاربری نیز ساخته می‌شود. ایمیل کسب و کار و شماره موبایلی که برای او ثبت می شود، برای مواقعی که لازم باشد خود آن کسب و کار در پنل مدیریتی خود وارد شود و برخی اقدامات را بر عهده بگیرد، ضروری است و صاحب کسب و کار می تواند با استفاده از آن رمز عبور خود را تعیین نماید. بنابراین صحت این موارد را کنترل نمایید.

```
    $param =
        [
        ## ========================= Required Parameters  ========================
            "_token_"               => API_TOKEN,      # Api_Token
            "username"            => 'USER NAME',
            "businessName"      => 'BUSINESS NAME',
            "email"                 => 'EMAIL',
            "guildCode"           => ['GUILD_CODE'],
            "country"              => 'COUNTRY',
            "state"                 => 'STATE',
            "city"                   => 'CITY',
            "address"             => 'ADDRESS',
            "description"         => 'DESCRIPTION',
            "agentFirstName"    => 'AGENT FIRST NAME',
            "agentLastName"    => 'AGENT LAST NAME',
            "agentCellphoneNumber"  => 'AGENT PHONE NUMBER',
    ## ======================== Optional Parameters  ===========================
#             "_token_issuer_"       => TOKEN_ISSUER,
#             "firstName"            => 'FIRST NAME',
#             "lastName"            => 'LAST NAME',
#             "sheba"                => 'SHEBA WITHOUT IR',
#             "nationalCode"        => 'CODE',
#             "economicCode"      => 'CODE',
#             "registrationNumber" => 'REGISTER NUMBER',
#             "cellphone"            => '09120000000',
#             "phone"                => '051322222222',
#             "fax"                   => 'FAX',
#             "postalCode"         => '9185175673',
#             "newsReader"        => 'true/false',
#             "logoImage"          => 'LOGO',
#             "coverImage"         => 'COVER',
#             "tags"                 => 'TAG1,TAG2',
#             "tagTrees"           => 'TREE1,TREE2',
#             "tagTreeCategoryName"  => 'CATEGORY',
#             "link"                 => 'LINK',
#             "lat"                  => 0,
#             "lng"                 => 0,
#             "agentNationalCode"   => 'CODE',

    ];
    try {
        $result = $dealingService->addUserAndBusiness($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد addUserAndBusiness

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| username | string |  نام کاربری کسب و کار جدید | نکته
* منحصر به فرد، فاقد space و حتما با حروف انگلیسی ثبت گردد. |  اجباری |
| country | string |  کشور محل کسب و کار |  |  اجباری |
| agentCellphoneNumber | string |  شماره موبایل نماینده | نکته
* به صورت 09123456789 وارد شود |  اجباری |
| agentLastName | string |  نام خانوادگی نماینده |  |  اجباری |
| agentFirstName | string |  نام نماینده |  |  اجباری |
| description | string |  توضیحات |  |  اجباری |
| address | string |  آدرس محل کسب و کار |  |  اجباری |
| businessName | string |  نام کسب و کار |  |  اجباری |
| state | string |  استان محل کسب و کار |  |  اجباری |
| city | string |  شهر محل کسب و کار |  |  اجباری |
| email | string |  ایمیل | نکته
* فرمت باید به صورت email باشد |  اجباری |
| guildCode | array of string |  لیست کد اصناف |  |  اجباری |
| cellphone | string |  شماره موبایل نماینده کسب و کار | نکته
* به صورت 09123456789 وارد شود |  |
| tagTrees | string |  تگ های درختی | نکته
* با ، (ویرگول) موارد را از هم جدا کنید |  |
| firstName | string |  نام شخص نماینده کسب و کار |  |  |
| lastName | string |  نام خانوادگی شخص نماینده کسب و کار |  |  |
| sheba | string |  کد شبا حساب بانکی | نکته
* شبا که به صورت عددی وارد می شود. (بدون IR) |  |
| lng | number |  طول جغرافیایی |  |  |
| lat | number |  عرض جغرافیایی |  |  |
| link | string | Link | نکته
* لینک دسترسی به کسب و کار از طریق sso |  |
| tagTreeCategoryName | string |  دسته درخت تگ |  |  |
| coverImage | string |  کاور کسب و کار | نکته
* آدرس اینترنتی تصویر کاور کسب و کار که به صورت مستقیم در دسترس است |  |
| tags | string |  تگ های آیتم | نکته
* با ، (ویرگول) موارد را از هم جدا کنید |  |
| phone | string |  شماره تلفن | نکته
* شماره تلفن با پیش شماره وارد شود |  |
| logoImage | string |  لوگو کسب و کار | نکته
* آدرس اینترنتی تصویر لوگو کسب و کار که به صورت مستقیم در دسترس است |  |
| newsReader | string | News Reader | نکته
* محدود کردن دسترسی کسب و کار |  |
| nationalCode | string |  شناسه ملی کسب و کار | نکته
* کد 11 رقمی |  |
| economicCode | string |  کد اقتصادی کسب و کار |  |  |
| registrationNumber | string |  شماره ثبت کسب و کار |  |  |
| postalCode | string |  کد پستی | نکته
* کد پستی 10 رقمی |  |
| fax | string |  شماره فکس | نکته
* در صورت ورد همراه با پیش شماره وارد شود |  |
| agentNationalCode | string |  کد ملی نماینده | نکته
* کد ملی 10 رقمی و بدون خط تیره و فاصله |  |

<div class="box-end">
</div>

## listUserCreatedBusiness

 با استفاده از این تابع می توانید لیست کسب و کارهایی را که ثبت کرده اید دریافت کنید یا در میان آن ها جستجو انجام دهید.

```

    $param =
        [
        ## ========================= Required Parameters  =========================
            "_token_"               => API_TOKEN,  # Api_Token
        ## ========================= Optional Parameters  =========================
#            "_token_issuer_"        => TOKEN_ISSUER,
#            "bizId"                 => 'BUSINESS ID',
#            "username"              => 'USER NAME',
#            "businessName"          => 'BUSINESS NAME',
#            "email"                 => 'EMAIL',
#            "guildCode"             => ['GUILD_CODE'],   # &#x644;&#x6CC;&#x633;&#x62A; &#x6A9;&#x62F; &#x635;&#x646;&#x641; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
#            "country"               => 'COUNTRY',
#            "state"                 => 'STATE',
#            "city"                  => 'CITY',
#            "active"                => true | false,
#            "offset"                => OFFSET,
#            "size"                  => SIZE,
#            "ssoId"                 => 'SSO ID',             # &#x634;&#x646;&#x627;&#x633;&#x647; sso &#x6A9;&#x627;&#x631;&#x628;&#x631;
#            "query"                 => 'QUERY',            # &#x645;&#x648;&#x631;&#x62F; &#x62C;&#x633;&#x62A;&#x62C;&#x648; &#x631;&#x648;&#x6CC; &#x628;&#x6CC;&#x632;&#x6CC;&#x646;&#x633; &#x647;&#x627;&#x6CC; &#x645;&#x648;&#x62C;&#x648;&#x62F;
#            "sheba"                 => 'SHEBA WITHOUT IR',
#            "nationalCode"          => 'CODE',
#            "economicCode"          => 'CODE',
#            "cellphone"             => '09120000000',
#            "tags"                  => ['TAG1', 'TAG2'],            # &#x644;&#x6CC;&#x633;&#x62A; &#x62A;&#x6AF;
#            "tagTrees"              => ['TREE1', 'TREE2'],              # &#x644;&#x6CC;&#x633;&#x62A; &#x62F;&#x631;&#x62E;&#x62A; &#x62A;&#x6AF;

    ];
    try {
        $result = $dealingService->listUserCreatedBusiness($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد listUserCreatedBusiness

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| bizId | array of integer |  شناسه کسب و کار |  |  |
| city | string |  نام شهر |  |  |
| email | string |  آدرس ایمیل کاربر | نکته
* فرمت باید به صورت email باشد |  |
| economicCode | string |  کد اقتصادی کسب و کار |  |  |
| nationalCode | string |  شناسه ملی کسب و کار |  |  |
| sheba | string |  کد شبا حساب بانکی | نکته
* شبا که به صورت عددی وارد می شود. (بدون IR) |  |
| businessName | string |  نام کسب و کار |  |  |
| username | string |  نام کاربری |  |  |
| ssoId | string |  شناسه sso کاربر |  |  |
| state | string |  نام استان |  |  |
| guildCode | array of string |  لیست کد اصناف |  |  |
| country | string |  نام کشور |  |  |
| active | string |  وضعیت |  |  |
| tagTrees | array of string |  لیست درخت تگ |  |  |
| tags | array of string |  لیست تگ |  |  |
| query | string |  مورد جستجو روی بیزینس های موجود |  |  |
| size | integer |  تعداد رکورد در هر صفحه |  |  |
| offset | integer |  اندیس شروع |  |  |
| cellphone | string |  شماره موبایل نماینده کسب و کار | نکته
* به صورت 09123456789 وارد شود |  |

<div class="box-end">
</div>

## updateBusiness
 با استفاده از این تابع می توانید اطلاعات کسب و کاری را که قبلا ثبت نموده اید ویرایش کنید

```

$param =
        [
        ## ===================== *Required Parameters  ======================
            "_token_"               => API_TOKEN,                 # Api_Token
            "bizId"                 => '{put business id}',                      # &#x634;&#x646;&#x627;&#x633;&#x647; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
            "businessName"          => 'BUSINESS NAME',             # &#x646;&#x627;&#x645; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
            "guildCode"             => ['GUILD_CODE'],              # &#x644;&#x6CC;&#x633;&#x62A; &#x6A9;&#x62F; &#x627;&#x635;&#x646;&#x627;&#x641;
            "country"               => 'COUNTRY',                            # &#x6A9;&#x634;&#x648;&#x631;
            "state"                 => 'STATE',                             # &#x627;&#x633;&#x62A;&#x627;&#x646;
            "city"                  => 'CITY',                                # &#x634;&#x647;&#x631;
            "address"               => 'ADDRESS',                            # &#x622;&#x62F;&#x631;&#x633;
            "description"           => 'DESCRIPTION',                     # &#x62A;&#x648;&#x636;&#x6CC;&#x62D;&#x627;&#x62A;
        ## ===================== Optional Parameters  =====================
#            "_token_issuer_"         => 1,
#            "email"                  => 'EMAIL',
#            "companyName"            => 'COMPANY NAME',            # &#x646;&#x627;&#x645; &#x634;&#x631;&#x6A9;&#x62A;
#            "shopName"               => 'SHOP NAME',               # &#x646;&#x627;&#x645; &#x641;&#x631;&#x648;&#x634;&#x6AF;&#x627;&#x647;
#            "shopNameEn"             => 'Shopping Center',         # &#x646;&#x627;&#x645; &#x627;&#x646;&#x6AF;&#x644;&#x6CC;&#x633;&#x6CC; &#x641;&#x631;&#x648;&#x634;&#x6AF;&#x627;&#x647;
#            "dateEstablishing"       => 'yyyy/mm/dd',              # &#x62A;&#x627;&#x631;&#x6CC;&#x62E; &#x634;&#x645;&#x633;&#x6CC; &#x62A;&#x627;&#x633;&#x6CC;&#x633; yyyy/mm/dd
#            "website"                => 'WEBSITE',                 # &#x648;&#x628;&#x633;&#x627;&#x6CC;&#x62A;
#            "sheba"                  => 'SHEBA',                   # &#x634;&#x628;&#x627; &#x6A9;&#x647; &#x628;&#x647; &#x635;&#x648;&#x631;&#x62A; &#x639;&#x62F;&#x62F;&#x6CC; &#x648;&#x627;&#x631;&#x62F; &#x645;&#x6CC; &#x634;&#x648;&#x62F;. (&#x628;&#x62F;&#x648;&#x646; IR)
#            "firstName"              => 'FIRST NAME',              # &#x646;&#x627;&#x645; &#x634;&#x62E;&#x635; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
#            "lastName"               => 'LAST NAME',               # &#x646;&#x627;&#x645; &#x62E;&#x627;&#x646;&#x648;&#x627;&#x62F;&#x6AF;&#x6CC; &#x634;&#x62E;&#x635; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
#            "nationalCode"           => 'CODE',                    # &#x634;&#x646;&#x627;&#x633;&#x647; &#x645;&#x644;&#x6CC; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
#            "economicCode"           => 'CODE',                    # &#x6A9;&#x62F; &#x627;&#x642;&#x62A;&#x635;&#x627;&#x62F;&#x6CC; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
#            "registrationNumber"     => 'REGISTER NUMBER',         # &#x634;&#x645;&#x627;&#x631;&#x647; &#x62B;&#x628;&#x62A; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
#            "cellphone"              => '09120000000',             # &#x634;&#x645;&#x627;&#x631;&#x647; &#x645;&#x648;&#x628;&#x627;&#x6CC;&#x644; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631;
#            "phone"                  => '02122222222',
#            "fax"                    => 'FAX',
#            "postalCode"             => 'POSTAL CODE',
#            "newsReader"             => 'true/false',
#            "changeLogo"             => 'LOGO',        # &#x62F;&#x631; &#x635;&#x648;&#x631;&#x62A;&#x6CC; &#x6A9;&#x647; &#x628;&#x62E;&#x648;&#x627;&#x647;&#x6CC;&#x62F; &#x62A;&#x635;&#x648;&#x6CC;&#x631; &#x644;&#x648;&#x6AF;&#x648; &#x631;&#x627; &#x62A;&#x63A;&#x6CC;&#x6CC;&#x631; &#x62F;&#x647;&#x6CC;&#x62F; true &#x648;&#x627;&#x631;&#x62F; &#x6A9;&#x646;&#x6CC;&#x62F;
#            "changeCover"            => 'COVER',       # &#x62F;&#x631; &#x635;&#x648;&#x631;&#x62A;&#x6CC; &#x6A9;&#x647; &#x628;&#x62E;&#x648;&#x627;&#x647;&#x6CC;&#x62F; &#x62A;&#x635;&#x648;&#x6CC;&#x631; &#x6A9;&#x627;&#x648;&#x631; &#x631;&#x627; &#x62A;&#x63A;&#x6CC;&#x6CC;&#x631; &#x62F;&#x647;&#x6CC;&#x62F; true &#x648;&#x627;&#x631;&#x62F; &#x6A9;&#x646;&#x6CC;&#x62F;
#            "logoImage"              => 'LOGO',          # logo image url
#            "coverImage"             => 'COVER',         # cover image url
#            "tags"                   => 'TAG1,TAG2',       # &#x62A;&#x6AF; &#x647;&#x627;&#x6CC; &#x622;&#x6CC;&#x62A;&#x645; &#x6A9;&#x647; &#x628;&#x627; , &#x627;&#x632; &#x647;&#x645; &#x62C;&#x62F;&#x627; &#x634;&#x62F;&#x647; &#x627;&#x646;&#x62F;
#            "tagTrees"               => 'TREE1,TREE2',
#            "tagTreeCategoryName"    => 'CATEGORY',   # &#x62F;&#x633;&#x62A;&#x647; &#x62F;&#x631;&#x62E;&#x62A; &#x62A;&#x6AF;
#            "link"                   => 'LINK',                  # &#x644;&#x6CC;&#x646;&#x6A9; &#x62F;&#x633;&#x62A;&#x631;&#x633;&#x6CC; &#x628;&#x647; &#x6A9;&#x633;&#x628; &#x648; &#x6A9;&#x627;&#x631; &#x627;&#x632; &#x637;&#x631;&#x6CC;&#x642; sso
#            "lat"                    => 0,
#            "lng"                    => 0,
#            "agentFirstName"         => 'FIRST NAME'         # &#x646;&#x627;&#x645; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647;
#            "agentLastName"          => 'LAST NAME'        # &#x646;&#x627;&#x645; &#x62E;&#x627;&#x646;&#x648;&#x627;&#x62F;&#x6AF;&#x6CC; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647;
#            "agentCellphoneNumber"   => 'MOBILE'            # &#x634;&#x645;&#x627;&#x631;&#x647; &#x62A;&#x644;&#x641;&#x646; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647;
#            "agentNationalCode"      => 'CODE'                # &#x6A9;&#x62F; &#x645;&#x644;&#x6CC; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647;
#            "changeAgent"            => true | false          # &#x62F;&#x631; &#x635;&#x648;&#x631;&#x62A;&#x6CC; &#x6A9;&#x647; &#x628;&#x62E;&#x648;&#x627;&#x647;&#x6CC;&#x62F; &#x646;&#x645;&#x627;&#x6CC;&#x646;&#x62F;&#x647; &#x631;&#x627; &#x62A;&#x63A;&#x6CC;&#x6CC;&#x631; &#x62F;&#x647;&#x6CC;&#x62F; true &#x648;&#x627;&#x631;&#x62F; &#x646;&#x645;&#x627;&#x6CC;&#x6CC;&#x62F;
    ];
    try {
        $result = $dealingService->updateBusiness($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد updateBusiness

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| bizId | integer |  شناسه کسب و کار |  |  اجباری |
| guildCode | array of string |  لیست کد اصناف |  |  اجباری |
| description | string |  توضیحات |  |  اجباری |
| address | string |  آدرس محل کسب و کار |  |  اجباری |
| city | string |  شهر محل کسب و کار |  |  اجباری |
| state | string |  استان محل کسب و کار |  |  اجباری |
| businessName | string |  نام کسب و کار |  |  اجباری |
| country | string |  کشور محل کسب و کار |  |  اجباری |
| lastName | string |  نام خانوادگی نماینده کسب و کار |  |  |
| changeLogo | string | Change Logo | نکته
* در صورتی که بخواهید تصویر لوگو را تغییر دهید true وارد کنید |  |
| agentNationalCode | string |  کد ملی نماینده | نکته
* کد ملی 10 رقمی و بدون خط تیره و فاصله |  |
| agentCellphoneNumber | string |  شماره موبایل نماینده | نکته
* به صورت 09123456789 وارد شود |  |
| agentLastName | string |  نام خانوادگی نماینده |  |  |
| agentFirstName | string |  نام نماینده |  |  |
| lng | number |  طول جغرافیایی |  |  |
| lat | number |  عرض جغرافیایی |  |  |
| link | string | Link | نکته
* لینک دسترسی به کسب و کار از طریق sso |  |
| tagTreeCategoryName | string |  دسته درخت تگ |  |  |
| tagTrees | string |  تگ های درختی | نکته
* با ، (ویرگول) موارد را از هم جدا کنید |  |
| tags | string |  تگ های آیتم | نکته
* با ، (ویرگول) موارد را از هم جدا کنید |  |
| coverImage | string |  کاور کسب و کار | نکته
* آدرس اینترنتی تصویر کاور کسب و کار که به صورت مستقیم در دسترس است |  |
| logoImage | string |  لوگو کسب و کار | نکته
* آدرس اینترنتی تصویر لوگو کسب و کار که به صورت مستقیم در دسترس است |  |
| changeCover | string | Change Cover | نکته
* در صورتی که بخواهید تصویر کاور را تغییر دهید true وارد کنید |  |
| companyName | string |  نام شرکت |  |  |
| sheba | string |  کد شبا حساب بانکی | نکته
* شبا که به صورت عددی وارد می شود. (بدون IR) |  |
| shopName | string |  نام فروشگاه |  |  |
| shopNameEn | string |  نام انگلیسی فروشگاه |  |  |
| website | string |  آدرس وب سایت |  |  |
| dateEstablishing | string |  تاریخ تاسیس به صورت شمسی | نکته
* تاریخ به صورت yyyy/mm/dd وارد شود |  |
| postalCode | string |  کد پستی | نکته
* شماره تلفن با پیش شماره وارد شود |  |
| fax | string |  شماره فکس | نکته
* در صورت ورد همراه با پیش شماره وارد شود |  |
| phone | string |  شماره تلفن | نکته
* شماره تلفن با پیش شماره وارد شود |  |
| cellphone | string |  شماره موبایل نماینده کسب و کار | نکته
* به صورت 09123456789 وارد شود |  |
| firstName | string |  نام نماینده کسب و کار |  |  |
| registrationNumber | integer |  شماره ثبت کسب و کار |  |  |
| email | string |  ایمیل |  |  |
| economicCode | string |  کد اقتصادی کسب و کار |  |  |
| nationalCode | string |  شناسه ملی کسب و کار |  |  |
| changeAgent | string | Change Agent | نکته
* در صورتی که بخواهید اطلاعات نماینده را تغییر دهید true وارد نمایید |  |

<div class="box-end">
</div>

## getApiTokenForCreatedBusiness

 با استفاده از این تابع می توانید API TOKEN کسب و کاری را که ثبت کرده اید دریافت کنید

```

    $param =
        [
        ## =================== Required Parameters  ======================
            "_token_"               => API_TOKEN,  # Api_Token
            'businessId'            => '{put business id}',            # id of business
        ## ================== Optional Parameters  =======================
#            "_token_issuer_"        => TOKEN_ISSUER,
        ];
    try {
        $result = $dealingService->getApiTokenForCreatedBusiness($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد getApiTokenForCreatedBusiness

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| businessId | integer |  شناسه کسب و کار |  |  اجباری |

<div class="box-end">
</div>

##  rateBusiness

 کاربرانی که خرید موفق داشته باشند و دنبال کننده کسب و کار باشند، می توانند به کسب و کار مربوطه امتیاز دهند، برای ثبت امتیاز کسب و کار توکن دسترسی کاربر مورد نیاز است و از طریق سرویس زیر انجام می گیرد.  امتیاز عددی بین صفر تا ده است.

```
    $param =
        [
        ## ======================= *Required Parameters  ===========================
            "_token_"       => ACCESS_TOKEN,          # Access_Token
            'businessId'    => '{put business id}',        # id of business
            'rate'          => '{put rate, between 0 and 10}',              # [user rate between 0 and 10]
        ## ======================= Optional Parameters  ============================
#            "_token_issuer_"        => TOKEN_ISSUER,      # default is 1

        ];
    try {
        $result = $dealingService->rateBusiness($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد rateBusiness

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| businessId | integer |  شناسه کسب و کار |  |  اجباری |
| rate | integer |  امتیاز کاربر به کسب و کار | نکته
* حداقل 0 است
* حداکثر 10 است |  اجباری |

<div class="box-end">
</div>

## commentBusiness

 کاربران می توانند نظر خود را برای یک کسب و کار ثبت نمایند. برای این منظور از این تابع به همراه توکن دسترسی کاربر استفاده نمایید. علاوه بر آن، کسب و کار می تواند برای خودش نیز، نظر ثبت کند.

```
    $param =
        [
        ## ======================= Required Parameters  ==========================
            "_token_"       => ACCESS_TOKEN,            # Access_Token
            'businessId'    => '{put business id}',            # id of business
            'text'          => "COMMENT",       # [user rate between 0 and 10]
        ## ====================== Optional Parameters  ===========================
#            "_token_issuer_"        => TOKEN_ISSUER,          # default is 1
        ];
    try {
        $result = $dealingService->commentBusiness($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد commentBusiness

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| businessId | integer |  شناسه کسب و کار |  |  اجباری |
| text | string |  نظر کاربر در مورد کسب و کار |  |  اجباری |

<div class="box-end">
</div>

## businessFavorite

 با استفاده از سرویس زیر، کاربر می تواند کسب و کار را به لیست علاقمندی های خود اضافه کند

```

    $param =
        [
        ## ===================== *Required Parameters  =====================
            "_token_"               => ACCESS_TOKEN,      # Access_Token
            'businessId'            => '{put business id}',                # id of business
            'disfavorite'           => "true/false",        # or true
        ## =================== Optional Parameters  ========================
#            "_token_issuer_"        => TOKEN_ISSUER,      # default is 1

        ];
    try {
        $result = $dealingService->businessFavorite($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد businessFavorite

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| businessId | integer |  شناسه کسب و کار |  |  اجباری |
| disfavorite | string | Disfavorite | نکته
* اگر خالی یا false باشد، به علاقه مندی ها اضافه می شود و اگر true باشد، از علاقه مندی ها حذف میشود |  |

<div class="box-end">
</div>

##  userBusinessInfos

 برای دریافت اطلاعات مربوط به تعاملات کاربر با کسب و کارها می توان از تابع زیر استفاده نمود. در اینجا منظور از تعامل به عنوان مثال:

* 		امتیازی که کاربر به کسب وکار داده است
* 		آیا کاربر جاری کسب و کار را دنبال کرده است و یا خیر
* 		کسب و کار جزء لیست علاقمندی کاربر می باشد یا خیر

می باشد اگر توکن کسب وکار را در کد زیر استفاده نمایید، rateCount مربوطه در نتیجه مربوط به تعداد امتیازدهی کاربران مختلف خواهد بود و اگر توکن کاربر لاگین شده را استفاده نمایید، rateCount همیشه برابر با یک خواهد بود. چرا که هر کاربر تنها یک بار قادر به امتیازدهی خواهد بود و با هر بار فراخوانی جدید سرویس امتیازدهی، امتیاز جدید جایگزین امتیاز قبلی خواهد شد. و هم چنین مقدار rate برابر با میانگین امتیازهای ثبت شده می باشد که در صورت استفاده از توکن کاربر لاگین شده، مقدار عددی rate با myRate همیشه برابر خواهد بود.

```

    $param =
        [
        ## ===================== Required Parameters  ========================
            "_token_"   => {ACCESS_TOKEN | API_TOKEN},          # [ACCESS_TOKEN] &#x6CC;&#x627; [ACCESS_TOKEN]
            "id"        => ["id of business"],                  # id of business
        ## ==================== Optional Parameters  =========================
#            "_token_issuer_"        => TOKEN_ISSUER,          # default is 1
        ];
    try {
        $result = $dealingService->userBusinessInfos($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد userBusinessInfos

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| id | array of integer |  لیست شناسه های کسب و کار |  |  اجباری |

<div class="box-end">
</div>

## commentBusinessList

 با استفاده از این تابع می توانید نظرات ثبت شده را مشاهده کنید. اگر فراخوانی سرویس با توکن لاگین شده کاربر صورت پذیرد، تنها نظرات کاربر را در نتیجه برمی گرداند و اگر توکن کسب وکار باشد، کل نظرات ثبت شده برای کسب و کار را نمایش خواهد داد.

```

    $param =
        [
        ## ================== *Required Parameters  =======================
            "_token_"           =>{ACCESS_TOKEN | API_TOKEN},  # [API_TOKEN] &#x6CC;&#x627; [ACCESS_TOKEN]
            'businessId'        => "BUSINESS ID",               # id of business
            'offset'            => '{put offset}',                           # [user rate between 0 and 10]
        ## ================= Optional Parameters  =========================
            # "_token_issuer_"   => TOKEN_ISSUER,              # default is 1
            # "size": 10,
            # "firstId": ID,
            # "lastId" : ID,
        ];
    try {
        $result = $dealingService->commentBusinessList($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد commentBusinessList

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| businessId | integer |  شناسه کسب و کار |  |  اجباری |
| firstId | integer | First Id | نکته
* در صورتی که این فیلد وارد شود فیلدهای lastId و offset نباید وارد شوند و نتیجه صعودی مرتب می شود. |  |
| lastId | integer | Last Id | نکته
* در صورتی که این فیلد وارد شود فیلدهای firstId و offset نباید وارد شوند و نتیجه نزولی مرتب می شود |  |
| offset | integer | Offset | نکته
* در صورتی که این فیلد وارد شود فیلدهای lastId و firstId نباید وارد شوند و نتیجه نزولی مرتب می شود |  |
| size | integer | Size | نکته
* تعداد رکورد در هر صفحه |  |

<div class="box-end">
</div>

## confirmComment

  کسب و کار می تواند نظرات داده شده توسط کاربران را تایید یا رد نماید. دقت داشته باشید که API TOKEN شما باید توکن کسب و کاری باشد که نظر برای آن ثبت شده است.

```

    $param =
        [
        ## ==================== *Required Parameters  =========================
            "_token_"           => API_TOKEN,     # Api_Token
            'commentId'         => '{put comment id}',            # id of comment
        ## ==================== Optional Parameters  ==========================
#            "_token_issuer_"    => TOKEN_ISSUER,              # default is 1

        ];
    try {
        $result = $dealingService->confirmComment($param);
        print_r($result);
    } catch (ValidationException $e) {
        print_r($e->getResult());
        print_r($e->getErrorsAsArray());
    } catch (PodException $e) {
        print_r($e->getResult());
    }
```


لیست پارامترهای ورودی متد confirmComment

|  نام فیلد |  نوع |  عنوان |  توضیحات |  اجباری؟ |
| --- | --- | --- | --- | --- |
| commentId | integer |  شناسه نظر |  |  اجباری |

<div class="box-end">
</div>
