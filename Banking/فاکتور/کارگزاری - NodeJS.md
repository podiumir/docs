
# کارگزاری

**ماژول** **pod-dealing-service**

کسب و کار ها می تواند کسب و کارهای دیگری را که با آن ها همکاری دارند ثبت نام کنند. این امکان برای کارگزاران و کسب و کارهایی که به تسهیم درآمد نیاز دارند بسیار مفید است. همچنین کاربران می توانند کسب و کارها را دنبال کنند، به آن ها امتیاز دهند و در مورد آن ها نظر دهند تمامی این کارها با استفاده از توابع این ماژول انجام می شود.

**دریافت ماژول**

```
npm install pod-dealing-service
```


**ایجاد یک نمونه از ماژول:**

در صورتی که بخواهید به سرور تست (sandbox) وصل شوید باید از حالت دوم ایجاد سرویس استفاده کنید و مقدار پارامتر serverType را برابر با sandbox قرار دهید. در صورت نیاز مقدار پیش فرض tokenIssuer نیز در سازنده ماژول قابل تنظیم است.

```
const PodDealingService = require(‘pod-user-operations-service’)
let podDealingService= new PodDealingService ({});
// let podDealingService = new PodDealingService ({serverType: ‘sandbox’});
// let podDealingService = new PodDealingService ({tokenIssuer: 0 | 1});
```

<div class="box-end">
</div>

## توابع
1.  addUserAndBusiness
2.  listUserCreatedBusiness
3.  updateBusiness
4.  getApiTokenForCreatedBusiness
5.  rateBusiness
6.  commentBusiness
7.  businessFavorite
8.  userBusinessInfos
9.  commentBusinessList
10.  confirmComment
<div class="box-end">
</div>
##  addUserAndBusiness
 با استفاده از این تابع می توانید یک کسب و کار ثبت کنید. با این اقدام، همزمان با ثبت کسب و کار، پنل کاربری نیز ساخته می‌شود. ایمیل کسب و کار و شماره موبایلی که برای او ثبت می شود، برای مواقعی که لازم باشد خود آن کسب و کار در پنل مدیریتی خود وارد شود و برخی اقدامات را بر عهده بگیرد، ضروری است و صاحب کسب و کار می تواند با استفاده از آن رمز عبور خود را تعیین نماید. بنابراین صحت این موارد را کنترل نمایید.

```
let addUserAndBusinessData = {
  // ------ REQUIRED ------
  _token_: 'API TOKEN',
  username: 'USERNAME',
  businessName: 'NAME',
  email: 'TEST@TEST.COM',
  guildCode: ['GUILDCODE'],
  country: 'COUNTRY',
  state: 'STATE',
  city: 'CITY',
  address: 'ADDRESS',
  description: 'DESCRIPTION',
  agentFirstName: 'AGENT FIRST NAME',
  agentLastName: 'AGENT LAST NAME',
  agentCellphoneNumber: '09151111111'

  // ------ OPTIONAL ------
  // _token_issuer_: 1
  // firstName: 'FIRST NAME'
  // lastName: 'LAST NAME'
  // sheba: 'SHEBA WITHOUT IR'
  // nationalCode: 'CODE'
  // economicCode: 'CODE'
  // registrationNumber: 'REGISTER NUMBER'
  // cellphone: 'MOBILE'
  // phone: 'PHONE'
  // fax: 'FAX'
  // postalCode: 'POSTAL CODE'
  // description: 'DESCRIPTION'
  // newsReader: 'NEWS READER'
  // logoImage: 'LOGO'
  // coverImage: 'COVER'
  // tags: 'TAG1,TAG2'
  // tagTrees: 'TREE1,TREE2'
  // tagTreeCategoryName: 'CATEGORY'
  // link: 'LINK'
  // lat: 0
  // lng: 0
  // agentNationalCode: 'CODE'
};

podDealingService.addUserAndBusiness(addUserAndBusinessData)
  .then(function (result) {
    console.log('function: addUserAndBusiness ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error addUserAndBusiness ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235631977',
  errorCode: 0,
  count: 0,
  ott: '1bb96b21d0efb62',
  result:
   { id: 4804,
     name: 'NAME23',
     guilds: [ [Object] ],
     description: 'DESCRIPTION',
     address: 'ADDRESS',
     city: '',
     state: '',
     country: '',
     latitude: 0,
     longitude: 0,
     subscriptionCount: 0,
     subscribed: false,
     numOfComments: 0,
     rate: { rate: 0, rateCount: 0 },
     userId: 2380802,
     ssoId: '11139414',
     numOfProducts: 0,
     email: 'TEST2@TEST.COM',
     fullAddress: 'ADDRESS',
     tags: [],
     tagTrees: [],
     active: false,
     apiToken: '109583e9ea394a99a5f88ccef04c992d',
     agent:
      { id: 2061,
        firstName: 'AGENT FIRST NAME',
        lastName: 'AGENT LAST NAME',
        cellphoneNumber: '09151111111' },
     numOfLike: 0,
     numOfDislike: 0,
     username: 'USERNAME2' } }
```


<div class="box-end">
</div>

## listUserCreatedBusiness
 با استفاده از این تابع می توانید لیست کسب و کارهایی را که ثبت کرده اید دریافت کنید یا در میان آن ها جستجو انجام دهید.

```
let listUserCreatedBusinessData = {
  // ------ REQUIRED ------
  _token_: 'API TOKEN'

  // ------ OPTIONAL ------
  // _token_issuer_: 1
  // bizId: ID
  // guildCode: 'GUILD CODE'
  // offset: OFFSET
  // size: SIZE
  // query: 'query'
  // tags: ['TAG1', 'TAG2']
  // tagTrees: ['TREE1', 'TREE2']
  // active: 'ACTIVE'
  // country: 'COUNTRY'
  // city: 'CITY'
  // ssoId: ID
  // username: 'USERNAME'
  // businessName: 'BUSINESS NAME'
  // nationalCode: 'CODE'
  // email: 'TEST@TEST.COM'
  // cellphone: 'MOPBILE'
};
podDealingService.listUserCreatedBusiness(listUserCreatedBusinessData)
  .then(function (result) {
    console.log('function: listUserCreatedBusiness ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error listUserCreatedBusiness ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235637515',
  errorCode: 0,
  count: 2,
  ott: 'fb78b347f604e7df',
  result:
   [ { id: 4804,
       name: 'NAME23',
       guilds: [Object],
       description: 'DESCRIPTION',
       address: 'ADDRESS',
       city: '',
       state: '',
       country: '',
       latitude: 0,
       longitude: 0,
       subscriptionCount: 0,
       subscribed: false,
       numOfComments: 0,
       rate: [Object],
       userId: 2380802,
       ssoId: '11139414',
       numOfProducts: 0,
       email: 'TEST2@TEST.COM',
       fullAddress: 'ADDRESS',
       tags: [],
       tagTrees: [],
       active: false,
       agent: [Object],
       numOfLike: 0,
       numOfDislike: 0,
       username: 'USERNAME2' },
     { id: 4766,
       name: 'NAME2222',
       guilds: [],
       description: 'DESCRIPTION',
       address: 'ADDRESS',
       city: '',
       state: '',
       country: '',
       latitude: 0,
       longitude: 0,
       subscriptionCount: 0,
       subscribed: false,
       numOfComments: 5,
       rate: [Object],
       userId: 2344899,
       ssoId: '10918554',
       numOfProducts: 0,
       fullAddress: 'ADDRESS',
       tags: [],
       tagTrees: [],
       active: false,
       agent: [Object],
       numOfLike: 0,
       numOfDislike: 0,
       legalInfo: [Object],
       username: 'USERNAME' } ] }
```


<div class="box-end">
</div>

## updateBusiness
 با استفاده از این تابع می توانید اطلاعات کسب و کاری را که قبلا ثبت نموده اید ویرایش کنید

```
let updateBusinessData = {
  // ------ REQUIRED ------
  _token_: 'API TOKEN',
  bizId: 0,
  businessName: 'NAME2',
  guildCode: ['GUILD CODE'],
  country: 'COUNTRY',
  state: 'STATE',
  city: 'CITY',
  address: 'ADDRESS',
  description: 'DESCRIPTION'

  // ------ OPTIONAL ------
  // _token_issuer_: 1
  // companyName: 'COMPANY NAME'
  // shopName: 'NAME'
  // shopNameEn: 'NAME'
  // website: 'SITE'
  // dateEstablishing: 'YYYY/MM/DD'
  // firstName: 'FIRST NAME'
  // lastName: 'LAST NAME'
  // sheba: 'SHEBA'
  // nationalCode: 'CODE'
  // economicCode: 'CODE'
  // email: 'TEST@TEST.COM'
  // registrationNumber: 'REGISTRETION NUMBER'
  // cellphone: 'MOBILE'
  // phone: 'PHONE'
  // fax: 'FAX'
  // postalCode: 'CODE'
  // changeLogo: true | false
  // changeCover: true | false
  // logoImage: 'IMAGE'
  // coverImage: 'IMAGE'
  // tags: 'TAG1, TAG2'
  // tagTrees: 'TREE1, TREE2'
  // tagTreeCategoryName: 'CATEGORY'
  // link: 'LINK'
  // lat: LAT
  // lng: LNG
  // agentFirstName: 'FIRST NAME'
  // agentLastName: 'LAST NAME'
  // agentCellphoneNumber: 'MOBILE'
  // agentNationalCode: 'CODE'
  // changeAgent: true | false
};
podDealingService.updateBusiness(updateBusinessData)
  .then(function (result) {
    console.log('function: createPreInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error createPreInvoice ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235641490',
  errorCode: 0,
  count: 0,
  ott: 'c4edd9a3f5894f35',
  result:
   { id: 4766,
     name: 'NAME22222',
     guilds: [],
     description: 'DESCRIPTION',
     address: 'ADDRESS',
     city: '',
     state: '',
     country: '',
     latitude: 0,
     longitude: 0,
     subscriptionCount: 0,
     subscribed: false,
     numOfComments: 5,
     rate: { rate: 0, rateCount: 0 },
     userId: 2344899,
     ssoId: '10918554',
     numOfProducts: 0,
     fullAddress: 'ADDRESS',
     tags: [],
     tagTrees: [],
     active: false,
     agent:
      { id: 2022,
        firstName: 'AGENT FIRST NAME',
        lastName: 'AGENT LAST NAME',
        cellphoneNumber: '09151111111' },
     numOfLike: 0,
     numOfDislike: 0,
     legalInfo: { id: 861, dateEstablishing: 0 },
     username: 'USERNAME' } }
```


<div class="box-end">
</div>

## getApiTokenForCreatedBusiness

 با استفاده از این تابع می توانید API TOKEN کسب و کاری را که ثبت کرده اید دریافت کنید

```
let getApiTokenForCreatedBusinessData = {
  // ------ REQUIRED ------
  _token_: 'API TOKEN',
  businessId: 0

  // ------ OPTIONAL ------
  // _token_issuer_: 1
};

podDealingService.getApiTokenForCreatedBusiness(getApiTokenForCreatedBusinessData)
  .then(function (result) {
    console.log('function: getApiTokenForCreatedBusiness ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getApiTokenForCreatedBusiness ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235653218',
  errorCode: 0,
  count: 0,
  ott: '92bbe2f804b76f5',
  result:
   { business: { id: 4766, name: 'NAME22222', numOfProducts: 0, rate: [Object] },
     apiToken: '131d1facfa994f31a39a4bd69ceafd13',
     clientId: '9327444a9d4b266a7d6c1c76' } }
```


<div class="box-end">
</div>

## rateBusiness

 کاربرانی که خرید موفق داشته باشند و دنبال کننده کسب و کار باشند، می توانند به کسب و کار مربوطه امتیاز دهند، برای ثبت امتیاز کسب و کار توکن دسترسی کاربر مورد نیاز است و از طریق سرویس زیر انجام می گیرد.  امتیاز عددی بین صفر تا ده است.

```
let rateBusinessData = {
  // ------ REQUIRED ------
  _token_: 'ACCESS TOKEN',
  businessId: 0,
  rate: 0

  // ------ OPTIONAL ------
  // _token_issuer_: 1
};

podDealingService.rateBusiness(rateBusinessData)
  .then(function (result) {
    console.log('function: rateBusiness ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error rateBusiness ============>', error);
  });
```


<div class="box-end">
</div>

## commentBusiness

 کاربران می توانند نظر خود را برای یک کسب و کار ثبت نمایند. برای این منظور از این تابع به همراه توکن دسترسی کاربر استفاده نمایید. علاوه بر آن، کسب و کار می تواند برای خودش نیز، نظر ثبت کند.

```
let commentBusinessData = {
  // ------ REQUIRED ------
  _token_: 'ACCESS TOKEN',
  businessId: 0,
  text: 'THIS IS MY COMMENT!!!'

  // ------ OPTIONAL ------
  // _token_issuer_: 1

};

podDealingService.commentBusiness(commentBusinessData)
  .then(function (result) {
    console.log('function: commentBusiness ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error commentBusiness ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235661049',
  errorCode: 0,
  count: 0,
  ott: '1df917b39b6f256a',
  result: 761 }
```


<div class="box-end">
</div>

## businessFavorite
 با استفاده از سرویس زیر، کاربر می تواند کسب و کار را به لیست علاقمندی های خود اضافه کند

```
let businessFavoriteData = {
  // ------ REQUIRED ------
  _token_: 'ACCESS TOKEN',
  businessId: 0,
  disfavorite: false // or true

  // ------ OPTIONAL ------
  // _token_issuer_: 1
};
podDealingService.businessFavorite(businessFavoriteData)
  .then(function (result) {
    console.log('function: getInvoiceListAsFile ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error getInvoiceListAsFile ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235681579',
  errorCode: 0,
  count: 0,
  ott: '1fe4b80152166a9d',
  result: true }
```


<div class="box-end">
</div>

## userBusinessInfos

 برای دریافت اطلاعات مربوط به تعاملات کاربر با کسب و کارها می توان از تابع زیر استفاده نمود. در اینجا منظور از تعامل به عنوان مثال:

+ امتیازی که کاربر به کسب وکار داده است
+ آیا کاربر جاری کسب و کار را دنبال کرده است و یا خیر
+ کسب و کار جزء لیست علاقمندی کاربر می باشد یا خیر

می باشد اگر توکن کسب وکار را در کد زیر استفاده نمایید، rateCount مربوطه در نتیجه مربوط به تعداد امتیازدهی کاربران مختلف خواهد بود و اگر توکن کاربر لاگین شده را استفاده نمایید، rateCount همیشه برابر با یک خواهد بود. چرا که هر کاربر تنها یک بار قادر به امتیازدهی خواهد بود و با هر بار فراخوانی جدید سرویس امتیازدهی، امتیاز جدید جایگزین امتیاز قبلی خواهد شد. و هم چنین مقدار rate برابر با میانگین امتیازهای ثبت شده می باشد که در صورت استفاده از توکن کاربر لاگین شده، مقدار عددی rate با myRate همیشه برابر خواهد بود.

```
let userBusinessInfosData = {
  // ------ REQUIRED ------
  _token_: 'API TOKEN or ACCESS TOKEN',
  id: [0]

  // ------ OPTIONAL ------
  // _token_issuer_: 1
};

podDealingService.userBusinessInfos(userBusinessInfosData)
  .then(function (result) {
    console.log('function: userBusinessInfos ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error userBusinessInfos ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235689819',
  errorCode: 0,
  count: 0,
  ott: 'aac455ebe47d016e',
  result:
   [ { id: 4766,
       name: 'NAME22222',
       subscriptionCount: 0,
       subscribed: false,
       rate: [Object],
       favorite: false } ] }
```


<div class="box-end">
</div>

##  commentBusinessList

 با استفاده از این تابع می توانید نظرات ثبت شده را مشاهده کنید. اگر فراخوانی سرویس با توکن لاگین شده کاربر صورت پذیرد، تنها نظرات کاربر را در نتیجه برمی گرداند و اگر توکن کسب وکار باشد، کل نظرات ثبت شده برای کسب و کار را نمایش خواهد داد.

```
let commentBusinessListData = {
  // ------ REQUIRED ------
  _token_: 'API TOKEN OR ACCESS TOKEN',
  businessId: 0,
  offset: 0

  // ------ OPTIONAL ------
  // _token_issuer_: 1
  // size: SIZE
  // firstId: ID
  // lastId: ID
};
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235764041',
  errorCode: 0,
  count: 1,
  ott: '9fb8b1ac78a1a14c',
  result:
   [ { id: 743,
       text: 'THIS IS MY COMMENT!!!',
       timestamp: 1563015948498,
       user: [Object],
       confirmed: true,
       numOfLikes: 0,
       numOfComments: 0,
       liked: false } ] }
```


<div class="box-end">
</div>

## confirmComment

  کسب و کار می تواند نظرات داده شده توسط کاربران را تایید یا رد نماید. دقت داشته باشید که API TOKEN شما باید توکن کسب و کاری باشد که نظر برای آن ثبت شده است.

```
let confirmCommentData = {
  // ------ REQUIRED ------
  _token_: 'API TOKEN', // API TOKEN OF SUB BUSINESS
  commentId: 0

  // ------ OPTIONAL ------
  // _token_issuer_: 1
};
podDealingService.confirmComment(confirmCommentData)
  .then(function (result) {
    console.log('function: reduceInvoice ============>', result, '\n');
  })
  .catch(function (error) {
    console.log('error reduceInvoice ============>', error);
  });
```


نمونه خروجی:

```
{ hasError: false,
  messageId: 0,
  referenceNumber: '235829512',
  errorCode: 0,
  count: 0,
  ott: '64cb03da085b75fd',
  result: true }
```

<div class="box-end">
</div>
